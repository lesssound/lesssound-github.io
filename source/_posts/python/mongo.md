title: mongo
categories:
  - python
tags:
  - mongodb
date: 2021-09-23 15:57:55
---


{% codeblock "MongoDB 语法" lang:sh >folded %}
# db.users.find() select * from users
# db.users.find({"age" : 27}) select * from users where age = 27
# db.users.find({"username" : "joe", "age" : 27}) select * from users where "username" = "joe" and age = 27
# db.users.find({}, {"username" : 1, "email" : 1}) select username, email from users
# db.users.find({}, {"username" : 1, "_id" : 0}) // no case  // 即时加上了列筛选，_id也会返回；必须显式的阻止_id返回
# db.users.find({"age" : {"$gte" : 18, "$lte" : 30}}) select * from users where age >=18 and age <= 30 // $lt(<) $lte(<=) $gt(>) $gte(>=)
# db.users.find({"username" : {"$ne" : "joe"}}) select * from users where username <> "joe"
# db.users.find({"ticket_no" : {"$in" : [725, 542, 390]}}) select * from users where ticket_no in (725, 542, 390)
# db.users.find({"ticket_no" : {"$nin" : [725, 542, 390]}}) select * from users where ticket_no not in (725, 542, 390)
# db.users.find({"$or" : [{"ticket_no" : 725}, {"winner" : true}]}) select * form users where ticket_no = 725 or winner = true
# db.users.find({"id_num" : {"$mod" : [5, 1]}}) select * from users where (id_num mod 5) = 1
# db.users.find({"$not": {"age" : 27}}) select * from users where not (age = 27)
# db.users.find({"username" : {"$in" : [null], "$exists" : true}}) select * from users where username is null // 如果直接通过find({"username" : null})进行查询，那么连带"没有username"的纪录一并筛选出来
# db.users.find({"name" : /joey?/i}) // 正则查询，value是符合PCRE的表达式
# db.food.find({fruit : {$all : ["apple", "banana"]}}) // 对数组的查询, 字段fruit中，既包含"apple",又包含"banana"的纪录
# db.food.find({"fruit.2" : "peach"}) // 对数组的查询, 字段fruit中，第3个(从0开始)元素是peach的纪录
# db.food.find({"fruit" : {"$size" : 3}}) // 对数组的查询, 查询数组元素个数是3的记录，$size前面无法和其他的操作符复合使用
# db.users.findOne(criteria, {"comments" : {"$slice" : 10}}) // 对数组的查询，只返回数组comments中的前十条，还可以{"$slice" : -10}， {"$slice" : [23, 10]}; 分别返回最后10条，和中间10条
# db.people.find({"name.first" : "Joe", "name.last" : "Schmoe"})  // 嵌套查询
# db.blog.find({"comments" : {"$elemMatch" : {"author" : "joe", "score" : {"$gte" : 5}}}}) // 嵌套查询，仅当嵌套的元素是数组时使用,
# db.foo.find({"$where" : "this.x + this.y == 10"}) // 复杂的查询，$where当然是非常方便的，但效率低下。对于复杂查询，考虑的顺序应当是 正则 -> MapReduce -> $where
# db.foo.find({"$where" : "function() { return this.x + this.y == 10; }"}) // $where可以支持javascript函数作为查询条件
# db.foo.find().sort({"x" : 1}).limit(1).skip(10); // 返回第(10, 11]条，按"x"进行排序; 三个limit的顺序是任意的，应该尽量避免skip中使用large-number
{% endcodeblock %}

{% codeblock "Mac上导出MongoDB数据" lang:sh %}
# Mac install mongo tools
brew tap mongodb/brew
brew install mongodb-database-tools
mongoexport --host 127.0.0.1:27017 -u user -p passwd --authenticationDatabase admin --db dbname -c cname --forceTableScan  -o res.json
mongoexport --uri=mongodb://username:password@host:27017/ --authenticationDatabase=admin -d db -c collection -o result.json
{% endcodeblock %}


{% codeblock "Python 调用 MongoDB" lang:sh >folded %}
import pymongo

from settings import Config


class MongoAPI:
    def __init__(self, db='db', tablename='tablename'):
        self.uri = Config.MONGO_URI
        self.myclient = pymongo.MongoClient(self.uri)
        mydb = self.myclient[db]
        self.mycol = mydb[tablename]

    # values = {"abr": 1}
    def query(self, myquery={'name': "somename"}, values=None):
        return self.mycol.find(myquery, values)

    def save(self, data):
        try:
            self.mycol.insert_one(data)
            return True
        except Exception as err:
            print(err)
            return False

    def update(self, _id, _key, data):
        myquery = {'id': _id}
        newvalues = {"$set": {_key: data}}
        self.mycol.update_one(myquery, newvalues)
        print(f'update success {_id}')
        return True

    def quit(self):
        self.myclient.close()

{% endcodeblock %}
