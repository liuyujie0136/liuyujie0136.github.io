# NJU程序设计基础案例内容合并Bash脚本
```bash
#!/bin/bash

cd /home/test/share/C_NJU/
touch ../C_NJU.md
files=`ls`
for i in $files
do
	echo '##' $i '\n```C++' >> ../C_NJU.md
	cat $i >> ../C_NJU.md
	echo '```\n' >> ../C_NJU.md
done
exit 0
```
