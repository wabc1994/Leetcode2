# Hashmap
充当记录的角色情况,关系存储的是,key 是给定数组中的元素情况，然后进行遍历统计即可

Map.Entry<s1,s2>这种情况

对一个HashMap进行某一次map.entrySet(),可以得到所有的所有的Map.Entry

对一个数组进行统计的方法情况乳腺癌
```java
//学会上面的写法情况，意思是说当字典中有个某个键当时候就是用其value,
如果没有当话就使用默认的值即可

for(int n:nums){
            frequencyMap.put(n,frequencyMap.getOrDefault(n,0)+1);
        }
```

也可以写成上面这宗写法情况
```java
for(int i:nums){
            if(frequencyMap.containsKey(i)){
                frequencyMap.put(i,frequencyMap.get(i)+1);
            }  
         frequencyMap.put(i,1);
        }
```


## 实现O(1)的时间复杂度

只有题目中说明了O(1)的取键值对， 都是采用这种办法进行, Map<key,<key,value>>, key 对应Integer, <key,value> 在真实的代码中我们可以进行一系列的封装， 比如封装成为一个节点


有时候需要同链表进行结合使用,像这种情况删除和添加操作需要同时更新链表和hashmap中的操作，数据情况

[LRU](https://leetcode.com/problems/lru-cache/discuss/45922/JAVA-Easy-Version-To-Understand!!!!)
       