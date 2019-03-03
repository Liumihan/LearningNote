##### [CSV对于文件的操作](http://www.cnblogs.com/unnameable/p/7366437.html)

1. 文件的读取

   ```Python
   import csv
   csv_filepath = ''
   csv_reader = csv.reader(open(csv_filepath, 'r'))
   for row in csv_reader:
       print(row)
   ```

2. 文件的写入

   ```
   out = open(csv_filepath, 'a', newline='')
   csv_writer = csv.writer(out)
   csv_writer.writerow(['1', '2'])
   ```

   