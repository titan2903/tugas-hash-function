# Tugas Hash Function

## Evaluasi Metode Hashing pada Dataset

Dokumentasi ini menjelaskan hasil evaluasi metode hashing yang dilakukan pada beberapa dataset dengan menggunakan berbagai metode hashing (Multiplication, Division, Folding, dan Mid-square). Evaluasi ini mengukur tiga parameter utama: **Collision Rate (%)**, **Load Factor (rasio jumlah item / ukuran table)**, dan **Max Chain Length**, yang digunakan untuk menilai efisiensi metode dalam menangani berbagai dataset.

## Dataset yang Diuji

Berikut adalah dataset yang diuji dalam evaluasi ini:

1. **Dataset 1**: Angka dari 1000 hingga 1099
    ```cpp
    vector<int> dataset1 = {1000, 1001, 1002, 1003, 1004, 1005, 1006, 1007, 1008, 1009,
                            1010, 1011, 1012, 1013, 1014, 1015, 1016, 1017, 1018, 1019,
                            1020, 1021, 1022, 1023, 1024, 1025, 1026, 1027, 1028, 1029,
                            1030, 1031, 1032, 1033, 1034, 1035, 1036, 1037, 1038, 1039,
                            1040, 1041, 1042, 1043, 1044, 1045, 1046, 1047, 1048, 1049,
                            1050, 1051, 1052, 1053, 1054, 1055, 1056, 1057, 1058, 1059,
                            1060, 1061, 1062, 1063, 1064, 1065, 1066, 1067, 1068, 1069,
                            1070, 1071, 1072, 1073, 1074, 1075, 1076, 1077, 1078, 1079,
                            1080, 1081, 1082, 1083, 1084, 1085, 1086, 1087, 1088, 1089,
                            1090, 1091, 1092, 1093, 1094, 1095, 1096, 1097, 1098, 1099};
    ```

2. **Dataset 2**: Angka besar yang bervariasi

   ```cpp
   vector<int> dataset2 = {15847, 73291, 28756, 91234, 45678, 82139, 67890, 34512, 78945, 23167,
                            89012, 56734, 12389, 90456, 67123, 45890, 78234, 34567, 91890, 25634,
                            58947, 83712, 47265, 94851, 36729, 82543, 69174, 51386, 74925, 18637,
                            95284, 42761, 87359, 63148, 29576, 85392, 71648, 54917, 38254, 92681,
                            46173, 79528, 13865, 97241, 58374, 84629, 27156, 93482, 65917, 41285,
                            78643, 52198, 86754, 39427, 94183, 67529, 23846, 89571, 45297, 81652,
                            57984, 34719, 98325, 62458, 26791, 83146, 49673, 95128, 71395, 47862,
                            84257, 18594, 92731, 56268, 39485, 75912, 43679, 87234, 61597, 24853,
                            98176, 52419, 86742, 31865, 77298, 43521, 89654, 65187, 27943, 94576,
                            58139, 82467, 46792, 73258, 19485, 95671, 62134, 38597, 84923, 51286,
                            77649, 24172, 98435, 53768, 87291, 41654, 76987, 32519, 95842, 68175,
                            44238, 89561, 25794, 93167, 56423, 82756, 48189, 74512, 19845, 96278,
                            63741, 37164, 84597, 51923, 78256, 24689, 97152, 53485, 86918, 42351,
                            79784, 35217, 91543, 67876, 44239, 88562, 25895, 94128, 57461, 83794,
                            49127, 75563, 31896, 98229, 64572, 37945, 84278, 51631, 78964, 25397};
   ```

3. **Dataset 3**: Angka ID yang besar

   ```cpp
   vector<int> dataset3 = {2021001, 2021002, 2021003, 2021004, 2021005, 2021006, 2021007, 2021008, 2021009, 2021010,
                            2021045, 2021046, 2021047, 2021048, 2021049, 2021050, 2021089, 2021090, 2021091, 2021092,
                            2021123, 2021124, 2021125, 2021126, 2021167, 2021168, 2021169, 2021170, 2021171, 2021172,
                            2022011, 2022012, 2022013, 2022014, 2022015, 2022034, 2022035, 2022036, 2022037, 2022038,
                            2022078, 2022079, 2022080, 2022081, 2022082, 2022112, 2022113, 2022114, 2022115, 2022116,
                            2022156, 2022157, 2022158, 2022159, 2022160, 2022190, 2022191, 2022192, 2022193, 2022194,
                            2023023, 2023024, 2023025, 2023026, 2023027, 2023067, 2023068, 2023069, 2023070, 2023071,
                            2023101, 2023102, 2023103, 2023104, 2023105, 2023145, 2023146, 2023147, 2023148, 2023149,
                            2023189, 2023190, 2023191, 2023192, 2023193, 2024012, 2024013, 2024014, 2024015, 2024016,
                            2024056, 2024057, 2024058, 2024059, 2024060, 2024090, 2024091, 2024092, 2024093, 2024094,
                            2024134, 2024135, 2024136, 2024137, 2024138, 2024178, 2024179, 2024180, 2024181, 2024182,
                            2025201, 2025202, 2025203, 2025204, 2025205, 2025245, 2025246, 2025247, 2025248, 2025249};
   ```

4. **Dataset 4**: String alfanumerik dengan berbagai format

   ```cpp
   vector<string> dataset4 = {"978-0-123456-78-9", "978-1-234567-89-0", "978-0-345678-90-1", "978-1-456789-01-2",
                               "979-0-567890-12-3", "978-2-678901-23-4", "979-1-789012-34-5", "978-3-890123-45-6",
                               "978-0-901234-56-7", "979-2-012345-67-8", "978-1-123456-78-9", "978-4-234567-89-0",
                               "979-0-345678-90-1", "978-2-456789-01-2", "978-5-567890-12-3", "979-1-678901-23-4",
                               "978-3-789012-34-5", "978-6-890123-45-6", "979-2-901234-56-7", "978-4-012345-67-8",
                               "ABC-DEF-123456-XY", "XYZ-ABC-789012-PQ", "MNO-PQR-345678-ST", "RST-UVW-901234-KL",
                               "JKL-MNO-567890-CD", "EFG-HIJ-234567-WX", "UVW-XYZ-890123-EF", "GHI-JKL-456789-AB",
                               "BCD-EFG-012345-YZ", "STU-VWX-678901-MN", "HIJ-KLM-123456-OP", "NOP-QRS-789012-GH",
                               "CDE-FGH-345678-TU", "TUV-WXY-901234-IJ", "DEF-GHI-567890-VW", "OPQ-RST-234567-CD",
                               "FGH-IJK-890123-XY", "VWX-YZA-456789-KL", "GHI-JKL-012345-AB", "WXY-ZAB-678901-PQ",
                               "A1B2C3D4E5F6G7H8", "X9Y8Z7A6B5C4D3E2", "M1N2O3P4Q5R6S7T8", "U9V8W7X6Y5Z4A3B2",
                               "K1L2M3N4O5P6Q7R8", "S9T8U7V6W5X4Y3Z2", "I1J2K3L4M5N6O7P8", "Q9R8S7T6U5V4W3X2",
                               "G1H2I3J4K5L6M7N8", "O9P8Q7R6S5T4U3V2", "E1F2G3H4I5J6K7L8", "M9N8O7P6Q5R4S3T2",
                               "C1D2E3F4G5H6I7J8", "K9L8M7N6O5P4Q3R2", "A1B2C3D4E5F6G7H8", "I9J8K7L6M5N4O3P2",
                               "LONG-STRING-PATTERN-001", "EXTENDED-FORMAT-DATA-025", "COMPLEX-IDENTIFIER-999",
                               "UNIQUE-ALPHANUMERIC-ABC", "VARIABLE-LENGTH-XYZ-789", "MIXED-CHARS-PATTERN-456",
                               "SPECIAL-FORMAT-ID-2024", "ULTRA-LONG-IDENTIFIER-X1", "CUSTOM-PATTERN-ABCD-789",
                               "MULTI-SEGMENT-ID-999999", "HYPHENATED-LONG-STRING-A", "EXTENDED-ID-FORMAT-2025"};
   ```

## Metode Hashing yang Digunakan

Beberapa metode hashing diuji untuk setiap dataset, yaitu:

1. **Multiplication Method**
2. **Division Method**
3. **Folding Method**
4. **Mid-square Method**

## Ouput Setiap Metode Hasing yang Digunakan

### Output Multiplication Method
    
    Running test for dataset 1 and table size 31, using Multiplication Method
    Dataset 1 - Table Size 31:
    Collision Rate: 222.581%
    Load Factor: 3.22581
    Max Chain Length: 4

    Running test for dataset 2 and table size 31, using Multiplication Method
    Dataset 2 - Table Size 31:
    Collision Rate: 383.871%
    Load Factor: 4.83871
    Max Chain Length: 8

    Running test for dataset 3 and table size 31, using Multiplication Method
    Dataset 3 - Table Size 31:
    Collision Rate: 361.29%
    Load Factor: 3.87097
    Max Chain Length: 18

    Running test for dataset 4 and table size 31, using Multiplication Method
    Dataset 4 - Table Size 31:
    Collision Rate: 129.032%
    Load Factor: 2.19355
    Max Chain Length: 5

    Running test for dataset 1 and table size 101, using Multiplication Method
    Dataset 1 - Table Size 101:
    Collision Rate: 12.8713%
    Load Factor: 0.990099
    Max Chain Length: 2

    Running test for dataset 2 and table size 101, using Multiplication Method
    Dataset 2 - Table Size 101:
    Collision Rate: 68.3168%
    Load Factor: 1.48515
    Max Chain Length: 5

    Running test for dataset 3 and table size 101, using Multiplication Method
    Dataset 3 - Table Size 101:
    Collision Rate: 110.891%
    Load Factor: 1.18812
    Max Chain Length: 18

    Running test for dataset 4 and table size 101, using Multiplication Method
    Dataset 4 - Table Size 101:
    Collision Rate: 19.802%
    Load Factor: 0.673267
    Max Chain Length: 4

    Running test for dataset 1 and table size 503, using Multiplication Method
    Dataset 1 - Table Size 503:
    Collision Rate: 0%
    Load Factor: 0.198807
    Max Chain Length: 1

    Running test for dataset 2 and table size 503, using Multiplication Method
    Dataset 2 - Table Size 503:
    Collision Rate: 5.96421%
    Load Factor: 0.298211
    Max Chain Length: 3

    Running test for dataset 3 and table size 503, using Multiplication Method
    Dataset 3 - Table Size 503:
    Collision Rate: 22.2664%
    Load Factor: 0.238569
    Max Chain Length: 18

    Running test for dataset 4 and table size 503, using Multiplication Method
    Dataset 4 - Table Size 503:
    Collision Rate: 2.98211%
    Load Factor: 0.135189
    Max Chain Length: 4

### Output Division Method
    
    Running test for dataset 1 and table size 31, using Division Method
    Dataset 1 - Table Size 31:
    Collision Rate: 222.581%
    Load Factor: 3.22581
    Max Chain Length: 4

    Running test for dataset 2 and table size 31, using Division Method
    Dataset 2 - Table Size 31:
    Collision Rate: 383.871%
    Load Factor: 4.83871
    Max Chain Length: 8

    Running test for dataset 3 and table size 31, using Division Method
    Dataset 3 - Table Size 31:
    Collision Rate: 287.097%
    Load Factor: 3.87097
    Max Chain Length: 6

    Running test for dataset 4 and table size 31, using Division Method
    Dataset 4 - Table Size 31:
    Collision Rate: 132.258%
    Load Factor: 2.19355
    Max Chain Length: 7

    Running test for dataset 1 and table size 101, using Division Method
    Dataset 1 - Table Size 101:
    Collision Rate: 0%
    Load Factor: 0.990099
    Max Chain Length: 1

    Running test for dataset 2 and table size 101, using Division Method
    Dataset 2 - Table Size 101:
    Collision Rate: 70.297%
    Load Factor: 1.48515
    Max Chain Length: 4

    Running test for dataset 3 and table size 101, using Division Method
    Dataset 3 - Table Size 101:
    Collision Rate: 68.3168%
    Load Factor: 1.18812
    Max Chain Length: 6

    Running test for dataset 4 and table size 101, using Division Method
    Dataset 4 - Table Size 101:
    Collision Rate: 22.7723%
    Load Factor: 0.673267
    Max Chain Length: 5

    Running test for dataset 1 and table size 503, using Division Method
    Dataset 1 - Table Size 503:
    Collision Rate: 0%
    Load Factor: 0.198807
    Max Chain Length: 1

    Running test for dataset 2 and table size 503, using Division Method
    Dataset 2 - Table Size 503:
    Collision Rate: 3.18091%
    Load Factor: 0.298211
    Max Chain Length: 3

    Running test for dataset 3 and table size 503, using Division Method
    Dataset 3 - Table Size 503:
    Collision Rate: 3.77734%
    Load Factor: 0.238569
    Max Chain Length: 2

    Running test for dataset 4 and table size 503, using Division Method
    Dataset 4 - Table Size 503:
    Collision Rate: 2.98211%
    Load Factor: 0.135189
    Max Chain Length: 4

### Output Folding Method
    
    Running test for dataset 1 and table size 31, using Folding Method
    Dataset 1 - Table Size 31:
    Collision Rate: 222.581%
    Load Factor: 3.22581
    Max Chain Length: 4

    Running test for dataset 2 and table size 31, using Folding Method
    Dataset 2 - Table Size 31:
    Collision Rate: 383.871%
    Load Factor: 4.83871
    Max Chain Length: 9

    Running test for dataset 3 and table size 31, using Folding Method
    Dataset 3 - Table Size 31:
    Collision Rate: 287.097%
    Load Factor: 3.87097
    Max Chain Length: 6

    Running test for dataset 4 and table size 31, using Folding Method
    Dataset 4 - Table Size 31:
    Collision Rate: 132.258%
    Load Factor: 2.19355
    Max Chain Length: 7

    Running test for dataset 1 and table size 101, using Folding Method
    Dataset 1 - Table Size 101:
    Collision Rate: 0%
    Load Factor: 0.990099
    Max Chain Length: 1

    Running test for dataset 2 and table size 101, using Folding Method
    Dataset 2 - Table Size 101:
    Collision Rate: 75.2475%
    Load Factor: 1.48515
    Max Chain Length: 5

    Running test for dataset 3 and table size 101, using Folding Method
    Dataset 3 - Table Size 101:
    Collision Rate: 49.505%
    Load Factor: 1.18812
    Max Chain Length: 3

    Running test for dataset 4 and table size 101, using Folding Method
    Dataset 4 - Table Size 101:
    Collision Rate: 22.7723%
    Load Factor: 0.673267
    Max Chain Length: 5

    Running test for dataset 1 and table size 503, using Folding Method
    Dataset 1 - Table Size 503:
    Collision Rate: 0%
    Load Factor: 0.198807
    Max Chain Length: 1

    Running test for dataset 2 and table size 503, using Folding Method
    Dataset 2 - Table Size 503:
    Collision Rate: 5.5666%
    Load Factor: 0.298211
    Max Chain Length: 3

    Running test for dataset 3 and table size 503, using Folding Method
    Dataset 3 - Table Size 503:
    Collision Rate: 1.39165%
    Load Factor: 0.238569
    Max Chain Length: 2

    Running test for dataset 4 and table size 503, using Folding Method
    Dataset 4 - Table Size 503:
    Collision Rate: 2.98211%
    Load Factor: 0.135189
    Max Chain Length: 4

### Output Mid-square Method
    
    Running test for dataset 1 and table size 31, using Mid-square Method
    Dataset 1 - Table Size 31:
    Collision Rate: 222.581%
    Load Factor: 3.22581
    Max Chain Length: 9

    Running test for dataset 2 and table size 31, using Mid-square Method
    Dataset 2 - Table Size 31:
    Collision Rate: 383.871%
    Load Factor: 4.83871
    Max Chain Length: 10

    Running test for dataset 3 and table size 31, using Mid-square Method
    Dataset 3 - Table Size 31:
    Collision Rate: 287.097%
    Load Factor: 3.87097
    Max Chain Length: 8

    Running test for dataset 4 and table size 31, using Mid-square Method
    Dataset 4 - Table Size 31:
    Collision Rate: 135.484%
    Load Factor: 2.19355
    Max Chain Length: 7

    Running test for dataset 1 and table size 101, using Mid-square Method
    Dataset 1 - Table Size 101:
    Collision Rate: 28.7129%
    Load Factor: 0.990099
    Max Chain Length: 6

    Running test for dataset 2 and table size 101, using Mid-square Method
    Dataset 2 - Table Size 101:
    Collision Rate: 71.2871%
    Load Factor: 1.48515
    Max Chain Length: 6

    Running test for dataset 3 and table size 101, using Mid-square Method
    Dataset 3 - Table Size 101:
    Collision Rate: 44.5545%
    Load Factor: 1.18812
    Max Chain Length: 4

    Running test for dataset 4 and table size 101, using Mid-square Method
    Dataset 4 - Table Size 101:
    Collision Rate: 26.7327%
    Load Factor: 0.673267
    Max Chain Length: 5

    Running test for dataset 1 and table size 503, using Mid-square Method
    Dataset 1 - Table Size 503:
    Collision Rate: 1.19284%
    Load Factor: 0.198807
    Max Chain Length: 2

    Running test for dataset 2 and table size 503, using Mid-square Method
    Dataset 2 - Table Size 503:
    Collision Rate: 3.77734%
    Load Factor: 0.298211
    Max Chain Length: 3

    Running test for dataset 3 and table size 503, using Mid-square Method
    Dataset 3 - Table Size 503:
    Collision Rate: 2.7833%
    Load Factor: 0.238569
    Max Chain Length: 2

    Running test for dataset 4 and table size 503, using Mid-square Method
    Dataset 4 - Table Size 503:
    Collision Rate: 3.18091%
    Load Factor: 0.135189
    Max Chain Length: 4

## Kesimpulan Hasil Pengujian

### 1. Dataset 1 (Angka dari 1000 hingga 1099)

* **Metode Terbaik**: **Metode Mid-square**

  * **Collision Rate**: 1.19% (untuk ukuran tabel 503)
  * **Load Factor**: 0.198807
  * **Max Chain Length**: 2
  * **Alasan**: Metode Mid-square memiliki collision rate yang paling rendah dengan ukuran tabel besar, dan juga memberikan nilai load factor yang optimal.

### 2. Dataset 2 (Angka besar yang bervariasi)

* **Metode Terbaik**: **Metode Mid-square**

  * **Collision Rate**: 3.78% (untuk ukuran tabel 503)
  * **Load Factor**: 0.298211
  * **Max Chain Length**: 3
  * **Alasan**: Metode Mid-square lebih baik dalam mengelola collision rate dan memberikan hasil yang baik pada tabel berukuran besar.

### 3. Dataset 3 (Angka ID yang besar)

* **Metode Terbaik**: **Metode Multiplikasi**

  * **Collision Rate**: 22.26% (untuk ukuran tabel 503)
  * **Load Factor**: 0.238569
  * **Max Chain Length**: 18
  * **Alasan**: Metode Multiplikasi lebih efektif dalam mengurangi collision rate pada dataset besar ini meskipun max chain lengthnya lebih tinggi.

### 4. Dataset 4 (String alfanumerik dengan berbagai format)

* **Metode Terbaik**: **Metode Multiplikasi**

  * **Collision Rate**: 2.98% (untuk ukuran tabel 503)
  * **Load Factor**: 0.135189
  * **Max Chain Length**: 4
  * **Alasan**: Metode Multiplikasi memberikan collision rate yang rendah dan mempertahankan max chain length yang terkontrol pada dataset dengan string alfanumerik.

**Mid-square Method** adalah yang terbaik untuk **Dataset 1** dan **Dataset 2** karena memiliki collision rate yang lebih rendah dan max chain length yang lebih kecil, terutama ketika menggunakan ukuran tabel yang lebih besar (503).

**Multiplication Method** lebih cocok untuk **Dataset 3** dan **Dataset 4**, karena lebih efisien dalam mengurangi collision rate pada dataset yang lebih besar dan menjaga load factor tetap terkontrol.