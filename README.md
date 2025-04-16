项目提案 3：基础日志文件解析与警报系统
标题：
基础日志文件解析与警报系统
网络安全概念：
日志分析 (Log Analysis)，威胁检测 (基于关键字)，审计 (Auditing) 基础。
C++ 概念：
类 (Class)，对象 (Object)，封装 (Encapsulation)，类函数 (Class Function)，文件 I/O (ifstream)，字符串处理 (string, getline, find)，循环 (while, for)，条件语句 (if)，函数 (Function)，std::vector (用于关键字)。
描述：
开发一个简单的程序，用于扫描日志文件并报告包含特定危险关键字的行。假定日志文件（例如 app.log）包含多行文本。 程序的核心任务是：
1. 读取文件： 打开指定的日志文件进行读取。需要处理文件无法打开的情况。
2. 关键字检查： 维护一个程序内部定义（硬编码）的警报关键字列表（例如，{"ERROR", "FATAL", "DENIED"}）。逐行读取日志文件。对于每一行，使用简单的字符串查找（如 string::find）检查该行是否包含列表中的任何一个关键字。
3. 打印警报： 如果某一行包含任何一个警报关键字，则将该完整行打印到控制台，并在前面加上 "ALERT:" 标识。 此项目重点在于练习基本的文件读取、循环遍历、条件判断以及字符串查找功能。可以使用一个简单的类（如 LogScanner）来组织代码，将关键字列表和扫描逻辑封装起来。
示例实现大纲：
1. 类： LogScanner
2.     成员变量： alertKeywords (std::vector<string>, 可在构造函数中初始化)
3.     构造函数： 初始化 alertKeywords
4.     类函数： scanFile (接收文件名，打开文件，逐行读取并检查关键字，打印警报)
1. 函数： main (创建 LogScanner 对象，获取文件名，调用 scanFile)
核心算法建议与伪代码：
1. 算法： 日志行关键字搜索算法 (Log Line Keyword Search Algorithm) - 实现 scanFile 类函数的核心逻辑。
2. Pseudocode:
METHOD scanFile (string filename)
    // Open the input file 'filename'
    IF file cannot be opened THEN
        PRINT error message
        RETURN
    END IF
 
    string line
    integer lineNum = 0
    // Read file line by line
    WHILE read line from file
        lineNum = lineNum + 1
        boolean alertTriggered = false
        // Check against all keywords
        FOR EACH keyword IN alertKeywords
            IF line CONTAINS keyword THEN
                alertTriggered = true
                BREAK FOR // Found a keyword, no need to check others for this line
            END IF
        END FOR
 
        // Print alert if triggered
        IF alertTriggered THEN
            PRINT "ALERT: Line " + lineNum + ": " + line
        END IF
    END WHILE
 
    // Close the file
END METHOD
