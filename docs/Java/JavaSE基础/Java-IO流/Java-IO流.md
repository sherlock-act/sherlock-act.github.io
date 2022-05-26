# Java-IO流

- Java中，对文件与目录进行操作的话可以使用File类进行，但是File类不能获取到文件里面的数据
- 所以就需要使用IO流
- IO流就是Input\Output的缩写，用于设备之间的数据传输；
- IO流的分类，重要流黄底标示

|    分类    |      字节输入流       |       字节输出流       |      字符输入流       |       字符输出流       |
| :--------: | :-------------------: | :--------------------: | :-------------------: | :--------------------: |
|  抽象基类  |    ==InputStream==    |    ==OutputStream==    |      ==Reader==       |       ==Writer==       |
|  访问文件  |  ==FileInputStream==  |  ==FileOutputStream==  |    ==FileReader==     |     ==FileWriter==     |
|  访问数组  | ByteArrayInputStream  | ByteArrayOutputStream  |    CharArrayReader    |    CharArrayWriter     |
|  访问管道  |   PipedInputStream    |   PipedOutputStream    |      PipedReader      |      PipedWriter       |
| 访问字符串 |                       |                        |     StringReader      |      StringWriter      |
|   缓冲流   | ==BufferInputStream== | ==BufferOutputStream== |   ==BufferReader==    |    ==BufferWriter==    |
|   转换流   |                       |                        | ==InputStreamReader== | ==OutputStreamWriter== |
|   对象流   | ==ObjectInputStream== | ==ObjectOutputStream== |                       |                        |
|            |   FilterInputStream   |   FilterOutputStream   |     FilterReader      |      FilterWriter      |
|   打印流   |                       |      PrintStream       |                       |      PrintWriter       |
| 推回输入流 |  PushbackInputStream  |                        |    PushbackReader     |                        |
|   数据流   |    DataInputStream    |    DataOutputStream    |                       |                        |