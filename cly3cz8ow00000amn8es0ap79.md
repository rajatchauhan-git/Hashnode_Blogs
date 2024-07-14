---
title: "Basic Linux Commands with a Twist"
datePublished: Mon Jul 01 2024 19:14:03 GMT+0000 (Coordinated Universal Time)
cuid: cly3cz8ow00000amn8es0ap79
slug: basic-linux-commands-with-a-twist
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719855700396/00cf0b12-9d86-4ecb-99b3-7f0b535c59cc.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1719861235644/d1668dbd-f065-4aa0-b6a2-af0798e7aa42.png
tags: linux, task, 90daysofdevops, trainwithshubham

---

## What are the Linux commands to:

**Task 1:** View the content of a file and display line numbers.

```bash
cat -n filename
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719856896091/2bdd5a35-ada6-4ad9-bb33-ada102edf61b.png align="center")

**Task 2:** Change the access permissions of files to make them readable, writable, and executable by the owner only.

```bash
chmod 777 filename
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719857046518/896f8f0f-e716-4259-abf1-7f79ae6aaa26.png align="center")

**Task 3:** Check the last 10 commands you have run.

```bash
history
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719857148153/af7a80a5-7b45-41ea-879e-dd90f7b93c00.png align="center")

**Task 4:** Remove a directory and all its contents.

```bash
rm -r directoryname
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719857626454/6327e5d9-9ed5-4713-ba43-5f572961a5ff.png align="center")

**Task 5:** Create a `fruits.txt` file, add content (one fruit per line), and display the content.  
  
\- Create file

```bash
touch fruits.txt
```

\- Add Content

```bash
vi fruits.txt
```

\- Display content

```bash
cat fruits.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719857924834/59823ea2-c391-4cae-b20d-4972d6af14cb.png align="center")

**Task 6:** Add content in `devops.txt` (one in each line) - Apple, Mango, Banana, Cherry, Kiwi, Orange, Guava. Then, append "Pineapple" to the end of the file.

\- Add Content

```bash
vi devops.txt
```

\- Append content in file

```bash
echo Pineapple >>devops.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719858549502/501b55af-f5f5-4cc2-a168-486b46cd4405.png align="center")

**Task 7:** Show the first three fruits from the file in reverse order.

```bash
head -n 3 devops.txt | tac
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719858847175/db1084d5-8235-4c92-ae73-e3bb02523a48.png align="center")

**Task 8:** Show the bottom three fruits from the file, and then sort them alphabetically.

```bash
tail -n 3 devops.txt | sort
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719858963281/6836c814-740d-46f8-83ac-3619795a23bd.png align="center")

**Task 9:** Create another file `Colors.txt`, add content (one color per line), and display the content.

```bash
cat Colors.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719859219613/1bac70a6-ba3c-4966-8056-440a6bb6f9d2.png align="center")

**Task 10:** Add content in `Colors.txt` (one in each line) - Red, Pink, White, Black, Blue, Orange, Purple, Grey. Then, prepend "Yellow" to the beginning of the file.

```bash
echo -e "Red\nPink\nWhite\nBlack\nBlue\nOrange\nPurple\nGrey" > Colors.txt
```

```bash
echo "Yellow" | cat - Colors.txt > temp && mv temp Colors.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719859808496/0b8183cb-47b8-44f2-b824-d50c7250a9ee.png align="center")

**Task 11:** Find and display the lines that are common between `fruits.txt` and `Colors.txt`

\- Sort the content of the "Colors.txt" and added them to "Colors\_sort.txt"

```bash
cat Colors.txt | sort >>Colors_sort.txt
```

\- Sort the content of the "fruits.txt" and added them to "fruits\_sort.txt"

```bash
cat fruits.txt | sort >>fruits_sort.txt
```

\- Find and display common lines in Colors\_sort.txt and fruits\_sort.txt

```bash
comm Colors_sort.txt fruits_sort.txt
```

\- Another way to find and display common lines in Colors\_sort.txt and fruits\_sort.txt

* The `-1` option suppresses the output of lines unique to the first file (`colors.txt`).
    
* The `-2` option suppresses the output of lines unique to the second file (`fruits.txt`).
    
* Combining `-12` means that only lines that are common to both files will be displayed.
    

```bash
comm -12 Colors_sort.txt fruits_sort.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719860529985/b40d0761-cbf8-46d1-9b2e-6009f59a2f85.png align="center")

**Task 12:** Count the number of lines, words, and characters in both `fruits.txt` and `Colors.txt`.

```bash
wc Colors.txt fruite.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719861118891/54a06edc-adb1-42cc-8fad-a73a966c3815.png align="center")

* **First column**: Number of lines.
    
* **Second column**: Number of words.
    
* **Third column**: Number of characters.
    
* **Last column**: Filename.