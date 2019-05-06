# Leetcode 721 账户合并
***
### 题目描述
给定一个列表`accounts`，每个元素`accounts[i]`是一个字符串列表，其中第一个元素`accounts[i][0]`是 *名称(name)*，其余元素是 *emails* 表示该账户的邮箱地址。  

现在，我们想合并这些账户。如果两个账户都有一些共同的邮件地址，则两个账户必定属于同一人。请注意，即使两个账户具有相同的名称，它们也可能属于不同的人，因为人们可能具有相同的名称。一个人最初可以拥有任意数量的账户，但其所有账户都具有相同的名称。  

合并账户后，按一下格式返回账户：每个账户的第一个元素是名称，其余元素是按顺序排列的邮箱地址。accounts 本身可以以任意顺序返回。   

**示例1:**   
	
	Input: 
	accounts = [["John", "johnsmith@mail.com", "john00@mail.com"], ["John", 	"johnnybravo@mail.com"], ["John", "johnsmith@mail.com", "john_newyork@mail.com"], ["Mary", 	"mary@mail.com"]]
	Output: [["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],  	["John", "johnnybravo@mail.com"], ["Mary", "mary@mail.com"]]
	Explanation: 
  		第一个和第三个 John 是同一个人，因为他们有共同的电子邮件 "johnsmith@mail.com"。 
  		第二个 John 和 Mary 是不同的人，因为他们的电子邮件地址没有被其他帐户使用。
  		我们可以以任何顺序返回这些列表，例如答案[['Mary'，'mary@mail.com']，		['John'，'johnnybravo@mail.com']，
  		['John'，'john00@mail.com'，'john_newyork@mail.com'，'johnsmith@mail.com']]仍然会被接受。

**注意：**

* `accounts`的长度将在`[1, 1000]`的范围内。
* `accounts[i]`的长度将在`[1, 10]`的范围内。
* `accounts[i][j]`的长度将在`[1, 30]`的范围内。

### 考点

* 并查集

### 思路
暴力解法会超时。- -

### 代码  
超时（仅供参考）

```
class Solution:
    def accountsMerge(self, accounts: List[List[str]]) -> List[List[str]]:
        i = 0
        for account in accounts:
            account[1:] = list(set(account[1:]))
        while i < len(accounts):
            flagi = 0
            flagj = 0
            mailsi = accounts[i][1:]
            for j in range(i + 1, len(accounts)):
                mailsj = accounts[j][1:]
                for maili in mailsi:
                    if maili in mailsj:
                        accounts.pop(j)
                        mailsi = list(set(mailsi + mailsj))
                        accounts[i][1:] = mailsi
                        flagj = 1
                        break
                if flagj == 1:
                    flagi = 1
                    break
            if flagi == 1:
                i -= 1
            i += 1
        for account in accounts:
            account[1:] = sorted(account[1:])

        return accounts
              
```

### Smart Solution(208ms)

```
class Solution:
 	"""并查集"""
    '''
    root 存放accounts里面每个节点的parent
    mail 存放每个邮箱地址的第一次出现parent
    '''
    def accountsMerge(self, accounts: List[List[str]]) -> List[List[str]]:
        root = [i for i in range(len(accounts))]
        mail = {}
        
        # 并查集find
        def find(i):
            if root[i] != i:
                return find(root[i])
            return root[i]
        
        
        for i in range(len(accounts)):
            for email in accounts[i][1:]:
                if email not in mail:
                    mail[email] = i
                else:
                    # 通过find找到i的最终parent，然后将parent的parent改写为mail通过find找到的parent
                    # 由于mail里存放的节点的父节点也可能被更新所以要通过find找到最终parent
                    
                    root[find(i)] = find(mail[email])
        
        # 存放子账户
        delt = set()
        for i in range(len(root)):
            if root[i] != i:
                # 通过find找到i的最终parent，然后把i添加进最终parent
                accounts[find(root[i])].extend(accounts[i][1:])
                delt.add(i)
        # 筛选出不含子账户的最终账户存入result
        result = []
        for i in range(len(accounts)):
            if i not in delt:
                result.append(accounts[i][:1]+sorted(list(set(accounts[i][1:]))))
        return result
```





	
