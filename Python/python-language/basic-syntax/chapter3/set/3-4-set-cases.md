# 集合案例

## 案例一：用户权限管理

```python
class PermissionSet:
    def __init__(self):
        self.users = {}

    def grant(self, user, *permissions):
        if user not in self.users:
            self.users[user] = set()
        self.users[user].update(permissions)

    def revoke(self, user, *permissions):
        if user in self.users:
            self.users[user].difference_update(permissions)

    def check(self, user, permission):
        return permission in self.users.get(user, set())

    def check_any(self, user, *permissions):
        return bool(self.users.get(user, set()) & set(permissions))

    def check_all(self, user, *permissions):
        return set(permissions).issubset(self.users.get(user, set()))

    def common_permissions(self, user1, user2):
        return self.users.get(user1, set()) & self.users.get(user2, set())

    def report(self):
        for user, perms in self.users.items():
            print(f"  {user}: {', '.join(sorted(perms))}")

ps = PermissionSet()
ps.grant("Alice", "read", "write", "delete")
ps.grant("Bob", "read", "write")
ps.grant("Charlie", "read")

print("用户权限:")
ps.report()

print(f"\nAlice 有 read 权限: {ps.check('Alice', 'read')}")
print(f"Alice 有 admin 权限: {ps.check('Alice', 'admin')}")
print(f"Alice 有 read 或 admin: {ps.check_any('Alice', 'read', 'admin')}")
print(f"Alice 同时有 read 和 write: {ps.check_all('Alice', 'read', 'write')}")

ps.revoke("Alice", "delete")
print(f"\n撤销 delete 后: {ps.users['Alice']}")
```

## 案例二：文本分析

```python
def analyze_text(text):
    words = text.lower().split()
    unique_words = set(words)
    word_counts = {}

    for word in words:
        word = word.strip(".,!?;:\"'()[]")
        if word:
            word_counts[word] = word_counts.get(word, 0) + 1

    return {
        "total_words": len(words),
        "unique_words": len(unique_words),
        "vocabulary": unique_words,
        "word_frequency": word_counts,
        "unused_letters": set("abcdefghijklmnopqrstuvwxyz") - set("".join(words))
    }

# Jaccard 相似度
def jaccard_similarity(set1, set2):
    return len(set1 & set2) / len(set1 | set2) if set1 | set2 else 0

text1 = "The quick brown fox jumps over the lazy dog"
text2 = "The quick brown fox jumps over the sleeping cat"

result1 = analyze_text(text1)
result2 = analyze_text(text2)

print(f"文本1单词数: {result1['total_words']}")
print(f"文本1不重复词: {result1['unique_words']}")
print(f"未使用的字母: {sorted(result1['unused_letters'])}")

similarity = jaccard_similarity(result1["vocabulary"], result2["vocabulary"])
print(f"两文本相似度: {similarity:.2%}")
```

## 案例三：社交网络好友关系

```python
class SocialNetwork:
    def __init__(self):
        self.friends = {}

    def add_friend(self, user, friend):
        self.friends.setdefault(user, set()).add(friend)
        self.friends.setdefault(friend, set()).add(user)

    def remove_friend(self, user, friend):
        self.friends.get(user, set()).discard(friend)
        self.friends.get(friend, set()).discard(user)

    def common_friends(self, user1, user2):
        return self.friends.get(user1, set()) & self.friends.get(user2, set())

    def suggest_friends(self, user):
        if user not in self.friends:
            return set()
        user_friends = self.friends[user]
        suggestions = set()
        for friend in user_friends:
            suggestions |= self.friends.get(friend, set())
        suggestions -= user_friends
        suggestions -= {user}
        return suggestions

    def friend_of_friend(self, user, degree=2):
        result = set()
        current = {user}
        for _ in range(degree):
            next_level = set()
            for u in current:
                next_level |= self.friends.get(u, set())
            result |= next_level
            current = next_level - result - {user}
        return result - {user}

    def mutual_friends(self, user):
        return self.friends.get(user, set())

# 创建网络
network = SocialNetwork()
pairs = [
    ("Alice", "Bob"), ("Alice", "Charlie"),
    ("Bob", "Diana"), ("Charlie", "Diana"),
    ("Diana", "Eve"), ("Bob", "Frank")
]

for u1, u2 in pairs:
    network.add_friend(u1, u2)

print("Alice 的好友:", network.mutual_friends("Alice"))
print("Alice 和 Bob 的共同好友:", network.common_friends("Alice", "Bob"))
print("Alice 可能认识的人:", network.suggest_friends("Alice"))
```

## 案例四：数据去重与分析

```python
def analyze_survey_data(responses):
    all_answers = set()
    common_answers = None

    for person, answers in responses:
        answer_set = set(answers)
        all_answers |= answer_set
        if common_answers is None:
            common_answers = answer_set
        else:
            common_answers &= answer_set

    return {
        "all": all_answers,
        "common": common_answers,
    }

survey = [
    ("Alice", ["Python", "Java", "SQL"]),
    ("Bob", ["Python", "JavaScript", "SQL", "Go"]),
    ("Charlie", ["Python", "SQL", "Rust"]),
    ("Diana", ["Python", "Go", "Java"]),
]

result = analyze_survey_data(survey)
print(f"所有出现的语言: {result['all']}")
print(f"所有人都会的语言: {result['common']}")

# 只被一个人会的语言
from collections import Counter
lang_counter = Counter()
for person, answers in survey:
    lang_counter.update(answers)

unique_langs = {lang for lang, count in lang_counter.items() if count == 1}
print(f"只有一个人会的语言: {unique_langs}")
```

## 案例五：缓存与标签系统

```python
import time

class TagCache:
    def __init__(self):
        self.tags = set()
        self.data = {}

    def add_item(self, item_id, tags):
        self.data[item_id] = set(tags)
        self.tags |= set(tags)

    def find_by_tags(self, required=None, optional=None):
        required = required or set()
        optional = optional or set()
        results = set()

        for item_id, item_tags in self.data.items():
            if required.issubset(item_tags):
                if not optional or item_tags & optional:
                    results.add(item_id)
        return results

    def find_by_any(self, tags):
        results = set()
        for item_id, item_tags in self.data.items():
            if item_tags & set(tags):
                results.add(item_id)
        return results

    def stats(self):
        tag_counts = {}
        for item_tags in self.data.values():
            for tag in item_tags:
                tag_counts[tag] = tag_counts.get(tag, 0) + 1
        return tag_counts

    def related_tags(self, tag):
        related = set()
        for item_tags in self.data.values():
            if tag in item_tags:
                related |= item_tags
        related.discard(tag)
        return related

cache = TagCache()
cache.add_item("doc1", ["python", "tutorial", "beginner"])
cache.add_item("doc2", ["python", "advanced", "web"])
cache.add_item("doc3", ["javascript", "web", "tutorial"])
cache.add_item("doc4", ["python", "data", "advanced"])

result = cache.find_by_tags(required={"python"}, optional={"tutorial"})
print(f"Python教程: {result}")

result = cache.find_by_any(["python", "javascript"])
print(f"Python或JS: {result}")

print(f"标签统计: {cache.stats()}")
print(f"与 'python' 相关: {cache.related_tags('python')}")
```
