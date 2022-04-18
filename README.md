# HR_Analytics_Job_change_final_project
## Descriptive Statistics
Berikut kesimpulan data yang kita dapat, sebagai berikut:
- Total data ada **19.158**
- Pada kolom `target` bisa diganti jadi booelan karena berupa binary 0 atau 1, atau bisa jadi object, menjadi stay or no.
- Terdapat kolom yang memiliki nilai kosong yaitu pada kolom `gender`, `enrolled_university`, `education_level`, `major_disciplin`, `experience`, `company_size`, `company_type`, dan `last_new_job`
- Kolom `enrollee_id` bisa dihapus karena hanya sebagai `identifier`
- Angka min pada kolom `city_development_index` jauh dengan median, malah median cenderung lebih dekat dengan max
- Pada kolom `training_hours`, nilai mean dan median cukup jauh gap nya, dan nilai max sangat jauh dari mean
- Pada kolom `city` memiliki kardinalitas (jumlah unique values) yang cukup tinggi (123), jadi bisa di drop
- Pada kolom `experience` memiliki kardinalitas (jumlah unique values) yang cukup tinggi (22), jadi bisa di drop
- Data dinominasi (proporsi lebih dari 50% dari jumlah baris data) oleh **STEM** (major_discipline), **memiliki pengalaman yang relevan** (relevent_experience), **tidak enrolled perguruan tinggi** (enrolled_university) dan didominasi oleh **Pria** (gender)
## Data Cleansing
Pada data yang akan kami olah terdapat kolom yang memiliki nilai kosong seperti pada kolom `gender`, `enrolled_university`, `education_level`, `major_discipline`, `experience`, `company_size`, `company_type`, dan `last_new_job`.
- `enrolled_university`, `education_level`, & `last_new_job` dapat di drop karena jumlahnya kecil (dibawah 5% dari jumlah total baris)
- `gender`: impute dengan nilai modus (Male)
- `major_discipline`: impute dengan nilai modus (STEM)
- `company_size`: impute dengan nilai modus (50-99)
- `company_type`: impute dengan nilai modus (Pvt Ltd)

Dari hasil diatas dapat kami pastikan bahwa data yang kami gunakan tidak memiliki data duplikat

Dikarenakan pada kolom city_development_index dan training_hours skewed maka diperlukan feature transformation agar mendekati normal. Pada city_development_index kami menggunakan skewnorm dikarenakan kolom tersebut skewed ke arah kiri (long-left tail).

Pada data diatas dilakukan standardization/normalization, fungsinya agar sebaran data mendekati normal.

Setelah itu kami melakukan value counts dan menyimpulkan bahwa:
- `gender`, `relevent_experience`, `enrolled_university`, & `education_level`: Label encoding
- `major_discipline`, `company_size`, `company_type`, `last_new_job`: One Hot Encoding

Pada data diatas kami menghilangkan class imbalance dengan cara Oversampling. 

## Modeling Experiment
Kami telah melakukan modelin beserta dengan evaluation dimana menghasilkan Model Random Forest sebagai model dengan recall paling tinggi yaitu 91% dengan akurasi Train Score **98%** dan Test Score **91%**

## Feature Importance
Kami menggunakan Model Random Forest dan di dapatkan feature importance seperti plot disamping. Dari plot tersebut kami melihat bahwa fitur training_hours dan city_development_index yang paling membantu model kita untuk membuat karyawan bertahan di perusahaan kami. 

Jika dijabarkan caranya adalah dengan:
- Meningkatkan lamanya training
- Membuka lowongan pekerjaan di tempat yang berpotensi yang memiliki city development tinggi dengan skala 75%
- Memberikan treatment kepada pelamar yang berasal dari kota tersebut.
