# 案例：银行账户管理系统

综合运用类与对象、实例方法、魔方方法、属性、异常等知识，构建一个完整的银行账户管理系统。

## 系统设计

```python
"""
银行账户管理系统
功能：开户、存款、取款、转账、查询、利息计算
"""
from datetime import datetime
from abc import ABC, abstractmethod
```

## 异常定义

```python
class AccountError(Exception):
    """账户异常基类"""
    pass

class InsufficientBalanceError(AccountError):
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        super().__init__(f"余额不足: 需 {amount:.2f}，仅 {balance:.2f}")

class NegativeAmountError(AccountError):
    def __init__(self, amount):
        super().__init__(f"金额不能为负: {amount}")

class AccountNotFoundError(AccountError):
    def __init__(self, account_id):
        super().__init__(f"账户不存在: {account_id}")
```

## 账户基类

```python
class Account:
    """账户基类"""

    # 类属性
    bank_name = "Python 银行"
    total_accounts = 0

    def __init__(self, owner, initial_balance=0):
        Account.total_accounts += 1
        self.account_id = f"{datetime.now():%Y%m%d}{Account.total_accounts:04d}"
        self.owner = owner
        self._balance = initial_balance
        self._transactions = []
        self._created_at = datetime.now()

        if initial_balance > 0:
            self._add_transaction("开户", initial_balance)

    def _add_transaction(self, trans_type, amount, target=None):
        """添加交易记录（内部方法）"""
        record = {
            "时间": datetime.now(),
            "类型": trans_type,
            "金额": amount,
            "余额": self._balance
        }
        if target:
            record["对方"] = target
        self._transactions.append(record)

    def deposit(self, amount):
        """存款"""
        if amount <= 0:
            raise NegativeAmountError(amount)
        self._balance += amount
        self._add_transaction("存款", amount)
        return self._balance

    def withdraw(self, amount):
        """取款"""
        if amount <= 0:
            raise NegativeAmountError(amount)
        if amount > self._balance:
            raise InsufficientBalanceError(self._balance, amount)
        self._balance -= amount
        self._add_transaction("取款", amount)
        return self._balance

    def get_balance(self):
        """查询余额"""
        return self._balance

    def transfer_to(self, target_account, amount):
        """转账"""
        if not isinstance(target_account, Account):
            raise TypeError("目标必须是 Account 实例")
        if amount <= 0:
            raise NegativeAmountError(amount)
        if amount > self._balance:
            raise InsufficientBalanceError(self._balance, amount)

        self._balance -= amount
        target_account._balance += amount

        self._add_transaction("转账", amount, target_account.owner)
        target_account._add_transaction("收款", amount, self.owner)

    def get_transactions(self, limit=10):
        """获取最近交易记录"""
        return self._transactions[-limit:]

    @abstractmethod
    def calculate_interest(self):
        """计算利息（子类实现）"""
        pass

    def __str__(self):
        return f"{self.owner} 的账户 [{self.account_id}]"

    def __repr__(self):
        return f"Account('{self.owner}', {self._balance})"

    def __len__(self):
        return len(self._transactions)

    def __contains__(self, amount):
        return 0 <= amount <= self._balance
```

## 储蓄账户

```python
class SavingsAccount(Account):
    """储蓄账户：按年利率计息"""

    # 类属性：利率表
    interest_rates = {
        "0-1年": 0.015,
        "1-3年": 0.025,
        "3年以上": 0.035
    }

    def __init__(self, owner, initial_balance=0, deposit_term="0-1年"):
        super().__init__(owner, initial_balance)
        self.deposit_term = deposit_term
        self.interest_rate = self.interest_rates.get(deposit_term, 0.015)

    def calculate_interest(self):
        """计算年利息"""
        return self._balance * self.interest_rate

    def apply_interest(self):
        """应用利息"""
        interest = self.calculate_interest()
        self._balance += interest
        self._add_transaction("利息", round(interest, 2))
        return interest

    def set_term(self, term):
        """设置存款期限"""
        if term in self.interest_rates:
            self.deposit_term = term
            self.interest_rate = self.interest_rates[term]

    def __str__(self):
        rate_pct = self.interest_rate * 100
        return (f"{self.owner} 的储蓄账户 [{self.account_id}] "
                f"利率 {rate_pct:.1f}% 余额 {self._balance:.2f}")
```

## 信用卡账户

```python
class CreditAccount(Account):
    """信用卡账户：可透支，有手续费"""

    def __init__(self, owner, initial_balance=0, credit_limit=5000):
        super().__init__(owner, initial_balance)
        self.credit_limit = credit_limit
        self.withdraw_fee_rate = 0.01  # 取款手续费率

    def get_available_balance(self):
        """获取可用额度"""
        return self._balance + self.credit_limit

    def withdraw(self, amount):
        """取款（含手续费）"""
        fee = amount * self.withdraw_fee_rate
        total = amount + fee
        available = self.get_available_balance()

        if amount <= 0:
            raise NegativeAmountError(amount)
        if total > available:
            raise InsufficientBalanceError(available, total)

        self._balance -= total
        self._add_transaction("取款", amount)
        if fee > 0:
            self._add_transaction("手续费", round(fee, 2))
        return self._balance

    def calculate_interest(self):
        """信用卡无利息，返回 0"""
        return 0

    def __str__(self):
        return (f"{self.owner} 的信用卡 [{self.account_id}] "
                f"可用 {self.get_available_balance():.2f}")
```

## 银行管理类

```python
class Bank:
    """银行管理系统"""

    def __init__(self, name="Python 银行"):
        self.name = name
        self._accounts = {}

    def create_savings_account(self, owner, initial=0, term="0-1年"):
        """创建储蓄账户"""
        account = SavingsAccount(owner, initial, term)
        self._accounts[account.account_id] = account
        print(f"开户成功: {account}")
        return account

    def create_credit_account(self, owner, initial=0, limit=5000):
        """创建信用卡"""
        account = CreditAccount(owner, initial, limit)
        self._accounts[account.account_id] = account
        print(f"开户成功: {account}")
        return account

    def get_account(self, account_id):
        """查找账户"""
        if account_id not in self._accounts:
            raise AccountNotFoundError(account_id)
        return self._accounts[account_id]

    def transfer(self, from_id, to_id, amount):
        """转账"""
        src = self.get_account(from_id)
        tgt = self.get_account(to_id)
        src.transfer_to(tgt, amount)
        print(f"转账成功: {src.owner} -> {tgt.owner} {amount:.2f}")

    def show_accounts(self):
        """显示所有账户"""
        print(f"\n{'='*50}")
        print(f"{self.name} - 账户列表")
        print(f"{'='*50}")
        for acc_id, acc in self._accounts.items():
            print(f"  {acc}")
        print(f"  共计 {len(self._accounts)} 个账户")
        print(f"{'='*50}\n")

    def __len__(self):
        return len(self._accounts)

    def __getitem__(self, account_id):
        return self.get_account(account_id)

    def __iter__(self):
        return iter(self._accounts.values())
```

## 运行演示

```python
def main():
    """演示银行系统"""
    bank = Bank()

    # 开户
    print("【开户】")
    alice = bank.create_savings_account("Alice", 10000, "1-3年")
    bob = bank.create_credit_account("Bob", 2000, limit=8000)
    charlie = bank.create_savings_account("Charlie", 5000)

    bank.show_accounts()

    # 存款取款
    print("【交易】")
    alice.deposit(5000)
    alice.withdraw(2000)
    print(f"Alice 余额: {alice.get_balance():.2f}")

    bob.withdraw(1000)
    print(f"Bob 可用额度: {bob.get_available_balance():.2f}")

    # 转账
    print("\n【转账】")
    bank.transfer(alice.account_id, charlie.account_id, 3000)

    # 利息
    print("\n【利息】")
    interest = alice.apply_interest()
    print(f"Alice 获得利息: {interest:.2f}，余额: {alice.get_balance():.2f}")

    # 魔方方法演示
    print("\n【魔方方法】")
    print(f"str(alice): {alice}")
    print(f"repr(alice): {repr(alice)}")
    print(f"alice 的交易记录数: {len(alice)}")
    print(f"5000 是否在 Alice 余额范围内: {5000 in alice}")
    print(f"50000 是否在 Alice 余额范围内: {50000 in alice}")

    # 异常处理
    print("\n【异常处理】")
    try:
        alice.withdraw(100000)
    except InsufficientBalanceError as e:
        print(f"取款失败: {e}")

    try:
        bank.transfer("nonexistent", alice.account_id, 100)
    except AccountNotFoundError as e:
        print(f"转账失败: {e}")

    # 遍历账户
    print("\n【遍历账户】")
    for account in bank:
        print(f"  - {account}")

    bank.show_accounts()

if __name__ == "__main__":
    main()
```
