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


/all-student (`getAllStudentsWithCourses()`)</br>
Profiler Result Comparison:
![](./assets/profiler-getAllStudentsWithCourses.png)

Jmeter Result:
![](./assets/jmeter-cli-all-student-after.png)


/all-student-name (`joinStudentNames()`)</br>
Profiler Result Comparion:
![](./assets/profiler-joinStudentNames.png)

Jmeter Result:
![](./assets/jmeter-cli-all-student-name-after.png)

/highest-gpa</br>
Profiler Result Comparion:
![](./assets/profiler-findStudentWithHighestGpa.png)

Jmeter Result:
![](./assets/jmeter-cli-highest-gpa-after.png)


Dari perbandingan hasil jmeter yang didapatkan, kita dapat melihat bahwa setiap endpoint mengalami penurunan latency namun ada beberapa endpoint yang tidak mengalami penurunan yang terlalu signifikan. Endpoint dengan penurunan yang paling signifikan adalah `/all-student`. Sebelum optimasi, latency untuk endpoint tersebut bernilai 25000-28000 ms, sedangkan setelah optimisasi bernilai 7000-8000. Endpoint `/all-students-name` juga mengalami penurunan yang signifikan dari 4000-5000 ms menjadi 250-450 ms setelah optimasi. Endpoint `/highest-gpa` mengalami penurunan namun tidak terlalu signifikan, dari 250-350 ms menjadi 250-300 ms.

# Reflection
> What is the difference between the approach of performance testing with JMeter and profiling with IntelliJ Profiler in the context of optimizing application performance?

JMeter menguji performa aplikasi dengan mensimulasikan beban eksternal melalui banyak permintaan secara concurrent untuk mengevaluasi latensi serta kemampuan respons sistem. Sedangkan IntelliJ Profiler menyediakan analisis rinci terkait penggunaan sumber daya, durasi eksekusi tiap fungsi atau metode, sehingga kita dapat mengidentifikasi bottleneck pada tingkat kode dan bagian mana yang perlu dioptimisasikan.

> How does the profiling process help you in identifying and understanding the weak points in your application?

Profiling membantu saya mengidentifikasi bagian mana dari kode saya (class, method atau function) yang menggunakan banyak resource. Untuk tutorial ini resource yang saya ukur adalah CPU time untuk mengetahui berapa lama yang dibutuhkan untuk sebuah kode selesai dijalankan. Namun metric-metric lain seperti memory usage dan CPU usage juga penting terutama untuk aplikasi scala besar. Dengan mengetahui kode mana yang menggunakan banyak resource, saya dapat fokus kepada kode tersebut untuk dioptimisasi. Jika kita lakukan tanpa profiling, maka kita hanya bisa menebak-nebak kode mana yang perlu dioptimisasi.

> Do you think IntelliJ Profiler is effective in assisting you to analyze and identify bottlenecks in your application code?

Iya. Intellij profiler menyediakan banyak fitur yang berguna seperti flame graph, timeline, dan method list. Semua fitur tersebut membantu kita untuk lebih mudah mencari kode mana yang memakan banyak resource. Selain itu Intellij profiler juga memiliki fitur comparison dimana hal tersebut membantu kita untuk dengan mudah membandingkan performance aplikasi kita sebelum dan sesudah kita melakukan refactoring atau optimization. 

> What are the main challenges you face when conducting performance testing and profiling, and how do you overcome these challenges?

Tantangan utama yang saya hadapi adalah hasil yang terkadang fluktuatif antar attempts. Contohnya pada satu attempt mungkin request kita hanya membutuhkan 130 ms namun ketika dicoba lagi tiba-tiba membutuhkan 190 ms. Tentu saja hasil antar attempt tidak mungkin sama persis, namun perbedaan yang cukup jauh dapat menyulitkan kita terutama ketika mengevaluasi hasil refactoring kita. Untuk mengatasinya, saya memutuskan untuk menjalankan testing dan profiling berkali-kali sampai saya melihat bahwa perbedaan hasil antar attempts tidak terlalu berbeda.

> What are the main benefits you gain from using IntelliJ Profiler for profiling your application code?

Keuntungan utama dari IntelliJ Profiler adalah fitur profilingnya yang lengkap. Seperti yang dijelaskan di pertanyaan refleksi sebelumnya, Intellij profiler menyediakan banyak fitur yang berguna seperti flame graph, timeline, dan method list. Semua fitur tersebut membantu kita untuk lebih mudah mencari kode mana yang memakan banyak resource. Hasil dari profiling tersebut juga di tampilkan secara baik yang memudahkan kita untuk mengidentifikasi bottleneck pada kode kita.

>  How do you handle situations where the results from profiling with IntelliJ Profiler are not entirely consistent with findings from performance testing using JMeter?

IntelliJ Profiler dan JMeter melakukan pengujian dengan metode yang berbeda. Pada JMeter kita mengirimkan request banyak secara concurrent kepada aplikasi kita. Maka jika hasil dari IntelliJ Profiler dan JMeter kita berbeda, salah satu kemungkinan alasannya adalah mungkin aplikasi kita tidak menerapkan concurrency dengan baik. Kita perlu menganalisa kode kita dan melakukan perbaikan dimana diperlukan. Selain itu kita juga dapat menjalankan JMeter dan IntelliJ profiler pada waktu yang sama dan membandingkan hasilnya. Dengan begitu kita dapat dengan lebih mudah mengidentifikasi sumber dari perbedaan hasil.

> What strategies do you implement in optimizing application code after analyzing results from performance testing and profiling? How do you ensure the changes you make do not affect the application's functionality?

Strategi optimisasi pertama yang saya lakukan adalah apabila sebuah fungsionalitas suatu potongan kode dapat digantikan oleh implementasi library java, ubahlah menjadi menggunakan library tersebut. Hal ini disebabkan karena implementasi dari library java tersebut biasanya lebih optimal dibandingkan implementasi yang kita buat sendiri. Setelah itu saya mencoba untuk meminimalisir repeated calls. Contohnya pada fungsi `getAllStudentsWithCourses()`, sebelum optimisasi kodenya adalah sebagai berikut

```java
    public List<StudentCourse> getAllStudentsWithCourses() {
        List<Student> students = studentRepository.findAll();
        List<StudentCourse> studentCourses = new ArrayList<>();
        for (Student student : students) {
            List<StudentCourse> studentCoursesByStudent = studentCourseRepository.findByStudentId(student.getId());
            for (StudentCourse studentCourseByStudent : studentCoursesByStudent) {
                StudentCourse studentCourse = new StudentCourse();
                studentCourse.setStudent(student);
                studentCourse.setCourse(studentCourseByStudent.getCourse());
                studentCourses.add(studentCourse);
            }
        }
        return studentCourses;
    }
```

fisini kita dapat lihat bahwa terjadi repeated calls terhadap fungsi `findByStudentId`. Repeated calls tersebut dapat dihindari dengan menggunakan `studentCourseRepository.findAll()` dimana secara implementasinya dapat retrieve semua data hanya dalam 1 query.

Untuk memastikan kebenaran dari kode hasil refactoring, saya lakukan secara manual yaitu memastikan outputnya sama setelah refactoring. Namun, kita dapat membuat unit tests yang akan membantu kita untuk cek output dari kodenya tanpa perlu kita lakukan secara manual. Hal ini meminimalisir kemungkinan human error terutama jika aplikasi kita merupakan aplikasi yang lebih rumit.













