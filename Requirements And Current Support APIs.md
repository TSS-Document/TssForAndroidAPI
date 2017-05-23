

# 老师用户
 ## 登录系统  

  有
```
/api/user/auth
```
  返回
```javascript
{
  id:233,
  username:"liuqin",
  name:"刘钦",
  type:"teacher",
  avatar:"",
  gender:"",
  email:"",
  schoolId:1
}
```

## 查看学生列表  

  有

  获取所有班级：
```
/api/group
```
  返回
```javascript
[
  {
    id:1,
    name:""
  }
]
```

  获取一个班级的学生列表：
```
/api/group/{groupId}/students
```
  返回
```javascript
[
  {
    id:22,
    username:"131250107",
    name:"雷莳芳",
    type:"student",
    avatar:"",
    gender:"",
    email:"",
    schoolId:1,
    gitId:12,
    gitUsername:"131250107"
    number:"131250107",
    groupId:2
  }
]
```

## 查看自己账户的作业、练习和考试列表

  有
```
  /api/course/{courseId}/exam
  /api/course/{courseId}/homework
  /api/course/{courseId}/exercise
```
  返回
```javascript
[
  {
    id:1,
    title:"考试1",
    description:"",
    startAt:"",
    endAt:"",
    course:1,
    status:"initSuccess",
    currentTime:"",
    questions:[
      id:1,
      title:"题目1",
      description:"",
      difficulty:"1",
      gitUrl:"xxx.git",
      type:"",
      creator:{
        id:233,
        username:"liuqin",
        name:"刘钦",
        type:"teacher",
        avatar:"",
        gender:"",
        email:"",
        schoolId:1
      },
      duration:1,
      link:33,
      knowledgeVos:[
        {
          id:1
        }
      ]
    ]
  }
]
```

## 查看某次作业、练习和考试学生分数段(可能需要班级分类)

  没有分数段，只能获得所有学生的分数，不能通过班级分类
```
  /api/assignment/{assignmentId}/score
```

  返回
```javascript
{
    assignmentId: 12,
    questions: [
      {
        questionInfo:{
          id: 1,
          title: "题目1",
          description: "xxxxx",
          type: "exam"
        },
        students:[
          {
            studentId: 227,
            studentName: "雷莳芳",
            studentNumber: "131250107",
            score: 100,
            scored: true
          }
        ]
      }
    ]
}
```

## 查看某次作业、练习和考试学生考试分析(测试用例通过情况等)(可能需要班级分类)

  目前还没有获取所有学生的考试分析的功能，不过有获取单个学生的考试分析的功能，因此扩展会比较容易。


# 学生用户
## 登录系统

  有
```
  /user/auth
```
  返回
  ```javascript
  {
    id:22,
    username:"131250107",
    name:"雷莳芳",
    type:"student",
    avatar:"",
    gender:"",
    email:"",
    schoolId:1,
    gitId:12,
    gitUsername:"131250107"
    number:"131250107",
    groupId:2
  }
  ```
## 查看老师账户的作业、练习和考试列表

  不理解为什么要通过老师账户来查看，可以根据课程来查看
```
/api/course/{courseId}/exam
/api/course/{courseId}/homework
/api/course/{courseId}/exercise
```
  返回与老师的一致

## 查看自己账户的作业、练习和考试列表的Readme文件

  没有

## 查看自己作业、练习和考试统计信息(平均分，总评得分)

  没有


## 查看某次作业、练习和考试学生考试分析(测试用例通过情况等)

  有，这个API可以返回该学生的得分，测试用例通过情况和统计分析
```
/assignment/{assignmentId}/student/{studentId}/analysis
```

  返回
```javascript
{
  studentId:227,
  assignmentId:12,
  questionResults:[
    questionId:1,
    questionTitle:"题目1",
    scoreResult:{
      git_url:"xxx.git",
      score:100,
      scored:true
    },
    testResult:{
      git_url:"xxx.git",
      compile_succeeded:true,
      tested:true,
      testcases:[
        name:"test1",
        passed:true
      ]
    },
    metricData:{
      git_url:"xxx.git",
      measured:true,
      total_line_count:158,
      comment_line_count:35,
      field_count:5,
      method_count:5,
      max_coc:2
    }
  ]
}
```
