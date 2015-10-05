### 1、获取所有学校 GetColleges
<big><pre>
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/GetColleges
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "colleges":[
        "北京理工大学"
    ]
}
</pre></big>

### 2、获取指定学校的所有院系 GetSchools
<big><pre>
请求参数：    college: String     // 学校名称，如：北京理工大学
返回：       JSON
URL 示例：   http://localhost/GetSchools
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "schools":[
        "计算机学院",
        "经济与管理学院"
    ]
}
</pre></big>

### 3、获取指定学校的某一院系的所有专业 GetMajors
<big><pre>
请求参数：    college: String     // 指定学校的学校名称，如：北京理工大学
             school: String      // 指定的院系，如：计算机学院
返回：       JSON
URL 示例：   http://localhost/GetMajors
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "majors":[
        "计算机科学与技术",
        "物联网"
    ]
}
</pre></big>

### 4、获取可选的年级 GetGrades
<big><pre>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/GetGrades
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "grades":[
        2014,
        2013,
        2012,
        2011
    ]
}
</pre></big>

### 5、获取指定学校的所有校区 GetCampuses
<big><pre>
请求参数：    college: String     // 学校名称，如：北京理工大学
返回：       JSON
URL 示例：   http://localhost/GetCampuses
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "campuses":[
        "良乡",
        "中关村"
    ]
}
</pre></big>

### 6、获取指定学校的所有地址 GetLocations
<big><pre>
请求参数：    college: String     // 学校名称，如：北京理工大学
             campus: String      // 校区名称，可选
返回：       JSON
URL 示例：   http://localhost/GetLocations
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "locations":[
        "新一",
        "三号楼"
    ]
}
</pre></big>
