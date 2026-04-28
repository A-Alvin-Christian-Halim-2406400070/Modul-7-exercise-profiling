# Before optimization

/all-students
![](./assets/all-students-graph-before.png)
![](./assets/all-students-summary-before.png)
![](./assets/all-students-table-before.png)
![](./assets/all-students-tree-before.png)

/all-students-name
![](./assets/all-students-name-graph-before.png)
![](./assets/all-students-name-table-before.png)
![](./assets/all-students-name-tree-before.png)
![](./assets/all-students-nname-summary-before.png)

/highest-gpa
![](./assets/highest-gpa-graph-before.png)
![](./assets/highest-gpa-summary-before.png)
![](./assets/highest-gpa-table-before.png)
![](./assets/highest-gpa-tree-before.png)

Using CLI:

/all-students
![](./assets/all-student-cli-before.png)
/all-students-name
![](./assets/all-students-name-cli-before.png)

/highest-gpa:
![](./assets/highest-gpa-cli-before.png)


# Flame graphs
/all-student
![](./assets/flame-all-students.png)

/all-student-name
![](./assets/flame-all-students-name.png)

/highest-gpa
![](./assets/flame-highest-gpa.png)

# After optimization


/all-student (`getAllStudentsWithCourses()`)
Profiler Result Comparison:
![](./assets/profiler-getAllStudentsWithCourses.png)

Jmeter Result:
![](./assets/jmeter-cli-all-student-after.png)


/all-student-name (`joinStudentNames()`)
Profiler Result Comparion:
![](./assets/profiler-joinStudentNames.png)

Jmeter Result:
![](./assets/jmeter-cli-all-student-name-after.png)

/highest-gpa
Profiler Result Comparion:
![](./assets/profiler-findStudentWithHighestGpa.png)

Jmeter Result:
![](./assets/jmeter-cli-highest-gpa-after.png)






