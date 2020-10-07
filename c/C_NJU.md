# 程序设计基础课程案例 @ NJU
> 文件内容合并操作由[Bash脚本](C_NJU_bash)完成

## calendar.cpp 
```c++
#include <iostream>
using namespace std;

int main()
{
	int iYear,iMonth,iWeek,iDay,n,j;
	do
	{
		cout << "请输入闰年年份:"; 
		cin >> iYear;
	}while (iYear%4 != 0 || iYear%100 == 0);
	do
	{
		cout << "请输入闰年月份:"; 
		cin >> iMonth;
	}while (iMonth<1 || iMonth>12);
	
	cout << "\t\t" << iYear << " 年 " << iMonth << " 月 " << endl;
	cout << "日\t一\t二\t三\t四\t五\t六" << endl;
	
	switch (iMonth)
	{
		case 1:n = 31;iYear--;iMonth = 13;break;
		case 3:case 5:case 7:case 8:case 10:case 12:n = 31;break;
		case 4:case 6:case 9:case 11:n = 30;break;
		case 2:n = 29;iYear--;iMonth = 14;break;
	}
	
	int c=iYear/100,y=iYear%100;

	iWeek = ((c/4)-2*c+y+(y/4)+(26*(iMonth+1)/10)) % 7; 
	for (j=1;j<iWeek+1;j++)
		cout << "\t";
	
	for (iDay=1;iDay<=n;iDay++)
	{
		iWeek = ((c/4)-2*c+y+(y/4)+(26*(iMonth+1)/10)+iDay-1) % 7; 
		cout << iDay <<"\t";
		if (iWeek==6)
			cout<<endl;
	}
	return 0;
}
```

## circle1.cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	int n,i,j,k,a;
	cin >> n;
	for (i=0;i<=2*n;i++)
	{
		for (j=0-n;j<=n;j++)
			if ((4*(i-n)*(i-n)+(j-n)*(j-n))<=4*n*n)
			 {
			     cout << "*";
			     a = j;
			     break;
			 } 
			else cout <<" ";
		for (k=j;k<=n;k++)
			cout <<" ";
		for (j=n;j<=3*n;j++)
			if (2*n-j==a)
			 {
			     cout <<"*";
			 } 
			else cout <<" ";
		cout << endl;
	}
	return 0;
}
```

## circle.cpp 
```C++
#include <iostream>
using namespace std;
#define RATIO 4
int main()
{
	char aaa[]="*",aab[]=" ";
	int n,i,j,k,a;
	cin >> n;
	for (i=0;i<=2*n;i++)
	{
		for (j=0-n;j<=n;j++)
			if ((RATIO*(i-n)*(i-n)+(j-n)*(j-n))<=RATIO*n*n)
			 {
			     cout << aaa;
			     a = j;
			     break;
			 } 
			else cout <<aab;
		for (k=j;k<=n;k++)
			cout <<aab;
		for (j=n;j<=4*n;j++)
			if (2*n-j==a)
			 {
			     cout <<aaa;
			 } 
			else cout <<aab;
		cout << endl;
	}
	return 0;
}
```

## OJ_2.4.cpp 
```C++
#include <iostream>
using namespace std;

int f(int n,int k);
int main()
{
	int n,k;
	while(cin >> n >> k)
	{
		cout <<f(n,k)<<endl;
	}
	return 0;
}

int f(int n,int k)
{
	int i;
	int a=0;
	if (n==0)
		return 1;
	else if (n==1)
		return 1;
	for (i=1;i<=k;i++)
	{
		if (n-i>=0)
			a += f(n-i,k);
	}	
	return a;
}
```

## OJ_5.1.cpp 
```C++
#include <iostream>
#include <cstring> 
using namespace std;
#define N 257 

int strcmp(const char myin[],const char myout[]);

int main()
{
	int num=0,j;
	char myin[N]={""},myout[N]={""};
	cin >> myin;
	while (myin[num])
		num++;
	for (j=0;j<num;j++)
		myout[j]=myin[num-1-j];
	if (strcmp(myin,myout) == 0)
		cout <<"Y";
	else cout <<"N";
	return 0;
}
```

## OJ_5.2.cpp 
```C++
#include <iostream>
#include <cstring> 
using namespace std;
#define N 200 

char *strcat(char myin[],const char myout[]);

int main()
{
	int num=0,j;
	char myin[N],myout[N];
	cin >> myin;
	while (myin[num])
		num++;
	for (j=0;j<num;j++)
		myout[j]=myin[num-1-j];
	cout << strcat(myin,myout);
	return 0;
}
```

## OJ_5.3.cpp 
```C++
#include <iostream>
using namespace std;
#define N 10000

int main()
{
	char key[N][60]={""};
	int i,a,b,c,d,n=0;
	cin >> key[n];
	while (cin)
	{
		i=0;a=0;b=0;c=0;d=0;
		while (key[n][i])
		{
			if (key[n][i]>='A' && key[n][i]<='Z')
				a=1;
			else if (key[n][i]>='a' && key[n][i]<='z')
				b=1;
			else if (key[n][i]>='0' && key[n][i]<='9')
				c=1;
			else if (key[n][i]=='~'||key[n][i]=='!'||key[n][i]=='@'||key[n][i]=='#'||key[n][i]=='$'||key[n][i]=='%'||key[n][i]=='^')
				d=1;
			i++;
		}
		if ((a+b+c+d)>=3 && i>=9 && i<=17)
			cout << "YES"<<endl;
		else cout << "NO"<<endl;
		n++;
		cin >> key[n];
	}
	return 0;
}
```

## as10_1.cpp 
```C++
#include <iostream>
using namespace std;
#define N 100

int main()
{
	int num=0,j;
	char myin[N],myout[N];
	cin >> myin;
	while (myin[num])
		num++;
	for (j=0;j<num;j++)
		myout[j]=myin[num-1-j];
	cout << myout;
	return 0;
}
```

## as10_2.cpp 
```C++
#include <iostream>
#include <cstring>
using namespace std;
#define N 16

int strcmp(const char mykey[],const char key[]);

int main()
{
	int flag=0;
	char mykey[N],key[N]={"lyj987654"};
	cout << "Please input your key:";
	while (flag<3)
	{
		cin >> mykey;
		if (strcmp(mykey,key) == 0)
		{
			cout << "Pass!";
			break;
		}
		else if (flag <2)
			cout << "Wrong! Please try again:";
		flag++;
	}
	if (flag == 3)
		cout << "Your turns are used up. Good Luck!";
	return 0;
}
```

## as11_1.cpp 
```C++
#include <iostream>
using namespace std;
#define N 100

int main()
{
	int i,j,k=0,t=0,m=0;
	int a1[N]={},a2[N]={},a3[N]={};
	bool flag=true;
	struct node
	{
		int content;
		node *next;
	};
	node *head=NULL;
	node *p=new node;
	head = p;
    cin>>p->content; 
	p->next=NULL;
	node *q=p;
	while (p->content != -2) //using -1 as the end of the first node &-2 as the end of the second node
	{
		if (p->content != -1 && flag)
			k++;
		if (p->content == -1)
			flag=false;
		p=new node;
		cin>>p->content;
		q->next=p;
		p->next=NULL;
		q=p;
		m++;
	}
	
	for (node *p=head; p!= NULL; p=p->next)
	{
		if (t<=k)
		{
			a1[t]=p->content;
			t++;
		}
		else
		{
			a2[t-k-1]=p->content;
			t++;
		}
	}
	
	for (i=0;i<k;i++)	//交集 
		for (j=0;j<m-k-1;j++)
			if (a1[i]==a2[j])
				cout << a1[i]<<" ";
	cout <<endl;
	
	for (i=0;i<k;i++)	//并集 
		a3[i]=a1[i];
	for (j=0;j<m-k-1;j++)
		a3[k+j]=a2[j];
	for (i=0;i<m-1;i++)
		for (j=i+1;j<m-1;j++)
			if (a3[i]==a3[j])
				a3[i]=-1;
	for (i=0;i<m-1;i++)
		if (a3[i] != -1)
			cout << a3[i] <<" ";
	cout <<endl;
	
	
	for (i=0;i<k;i++)	//差集 1-2 
	{
		flag=true;
		for (j=0;j<m-k-1;j++)
			if (a1[i]==a2[j])
				flag=false;
		if (flag)
			cout << a1[i]<<" ";
	}		
	cout <<endl;
	delete p;
	delete q;
	return 0;
}
```

## as11_2.cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	int i=0,j,k;
	cin >> k;
	struct node
	{
		int content;
		node *next;
	};
	node *head=NULL;
	node *p=new node;
	head = p;
    cin>>p->content;	
    p->next=NULL;
	node *q=p;
	while (p->content != -1) //using -1 to end
	{
		p=new node;
		cin>>p->content;
		q->next=p;
		p->next=NULL;
		q=p;
		i++;
	}
	node *t=head;
	for (j=1;j<i-k;j++)
		t=t->next;
	cout << t->content;
	delete p;
	delete q;
	delete t;
	return 0;
} 
```

## as1_1.cpp 
```C++
#include <iostream>
using namespace std;
int main()
{
	cout<<":)"<<endl;//该字符画的含义是微笑
	return 0;
}
```

## as1_2.cpp 
```C++
#include <iostream>
using namespace std;
int main()
{
	cout<<"请输入两个整数："<<endl;
	int a,b,c;
	cin>>a>>b;
	c=a*a+b*b;
	cout<<c<<endl;
	return 0;
}
```

## as1_3.cpp 
```C++
#include <iostream>
#include <iomanip>
using namespace std;
int main()
{
	double a,b,c,d;
	cout<<"请输入一元二次方程ax^2+b^x+c=0系数a,b,c"<<endl;
	cin>>a>>b>>c;
	d=b*b-4*a*c;
	cout<<setiosflags(ios::fixed)<<setprecision(2)<<d<<endl;
	return 0;
}
```

## as2_1.cpp 
```C++
#include <iostream>
#include <cmath>
using namespace std;
int main()
{
	int n,m;
	cout << "Please input n" << endl;
	cin >> n;
	m = abs(1-n);
    if (m>n)
	  cout << "|1-" << n << "| > " << n << "-1" << endl;
	else
	  cout << "|1-" << n << "| = " << n << "-1" << endl;
	return 0;
}
```

## as2_2.cpp 
```C++
#include <iostream>
#include <iomanip>
using namespace std;
int main()
{
	double x,y;
	cout << "请输入公里数x" << endl;
	cin >> x;
	if (x <= 3)
	  y = 9 + 1;
	else
	  y = 9 + 1 + 2.4 * (x-3);
	cout << "应付款" << fixed << setprecision(1) << y << "元" << endl;
	return 0; 

}
```

## as3_1.cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	int a,d,n,i,s = 0;
	cout << "请输入等差数列的项数n:";
	cin >> n;
	cout << "请输入等差数列的首项a:";
	cin >> a;
	cout << "请输入等差数列的公差d:";
	cin >> d;
	for (i = 1;i <= n;i++) 
	{
		s = s + a;
		a = a + d;
	}
	cout << "等差数列的和为:" << s << endl;
	return 0;
}
```

## as3_2.cpp 
```C++
#include <iostream>
#include <cmath>
#include <iomanip>
using namespace std;

int main()
{
	double x0,x1,x2=0;
	cout << "请输入一个数:";
	cin >> x0;
	x1 = x0;
	x2 = (2*x1+x0/pow(x1,2))/3;
	while (abs(x2-x1) > 0.000001)
	{
		x1 = x2;
		x2 = (2*x1+x0/pow(x1,2))/3;
	}
	cout << x0 << "的立方根为:" << fixed << setprecision(2) << x2;
	return 0; 
}
```

## as3_3.cpp 
```C++
#include <iostream>
#include <cmath> 
using namespace std;

int main()
{
	int n,i,j;
	cout << "请输入菱形行数:";
	cin >> n;
	for (i=1;i<=n;i++)
	{ 
	  for (j=1;j<=n;j++)
	  {
	  	if (j>=(n+1)/2-((n-1)/2-abs(i-(n+1)/2)) && j<=(n+1)/2+((n-1)/2-abs(i-(n+1)/2)))
	  	  cout << "*";
		else cout << " ";
	  }
	  cout << endl;
	}	
	return 0;
}
```

## as4_1.cpp 
```C++
#include <iostream>
using namespace std;

int compose(int n,int r)
{
	int i,a=1,b=1;
	for (i=r+1;i<=n;i++) a *= i;
	for (i=2;i<=n-r;i++) b *= i;
	return a/b;
}
int main()
{
	int n,r;
	cout << "本程序用于计算从n个数取r个数的所有选择个数。" << endl;
	cout <<"请输入n:" ;
	cin >> n;
	cout << "请输入r:";
	cin >> r;
	cout << "计算结果为:" << compose(n,r) <<endl;
	return 0;
}
```

## as4_2.cpp 
```C++
#include <iostream>
#include <cmath> 
using namespace std;
int CountDigit(int n); //声明函数 
int KthDigit(int n, int k);//声明函数 

int main()
{
	int n,m;
	cout << "请输入正整数n:";
	cin >> n;
	m = CountDigit(n);//调用函数 
	cout <<"这是一个"<<m<<"位数。其右起第" << m/2 << "位上数字是:" << KthDigit(n,m/2) <<endl;//调用函数 
	return 0; 
}

int CountDigit(int n)//定义函数 
{
	int i;
	for (i=1;i<=n;i++)
	{
		n = n / 10;
		if (n < 10) break;
	}
	return i+1;
}

int KthDigit(int n, int k) //定义函数 
{
	n = n % (int)pow((double)10, k);
	n = n / pow((double)10, k-1);
	return n;
}
```

## as5_1.cpp 
```C++
#include <iostream>
using namespace std;

int IntRevs(int n);
int myPow(int n,int k);

int main()
{
	int n;
	cout << "请输入一个正整数:";
	cin >> n;
	cout << "该正整数的逆序数为:" << IntRevs(n) << endl;
	return 0;
}

int myPow(int n,int k)
{
	int i,p=1;
	for (i=1;i<=k;i++)
		p = p * n;
	return p;
}

int IntRevs(int n)
{
	int i,j,t,k=0,m=0;
	t = n;
	for (i=1;i<=t;i++)
	{
		t = t / 10;
		if (t < 10)  break;
	}
	k = i + 1;
	for (j=1;j<=i+1;j++)
	{
		m = m + ( n % 10) * myPow(10,k-1);
		n = n / 10;
		k = k - 1;  
	}
	return m;
}
```

## as5_2.cpp 
```C++
#include <iostream>
using namespace std;

int IntRevsR(int n);
int myPow(int n,int k);

int main()
{
	int n;
	cout << "请输入一个正整数:";
	cin >> n;
	cout << "该正整数的逆序数为:" << IntRevsR(n) << endl;
	return 0;
}

int myPow(int n,int k)
{
	int i,p=1;
	for (i=1;i<=k;i++)
		p = p * n;
	return p;
}

int IntRevsR(int n)
{
	int i,k,m,t=n;
	for (i=1;i<=t;i++)
	{
		t = t / 10;
		if (t < 10)  break;
	}
	k = i + 1;
	if ( n < 10 )
		return n;
	else
	{
		m = n % 10;
		n = n / 10;	
		return IntRevsR(n)+m*myPow(10,k-1);
	}
}
```

## as6_1.cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	char x,y;
	cin >> x;
	y = x - 32;
	cout << y;
	return 0;
}
```

## as6_2.cpp 
```C++
#include <iostream>
using namespace std;

bool zhishu(int i);

int main()
{
	int a,i,j;
	cin >> a;
	for (i=2;i<=a;i++) 
	{
		j = 0;
		if (zhishu(i))
		{
			while (a % i == 0)
			{
				j = j + 1;
				a = a / i;
			}
			if (j != 0)
				cout << i << "(" << j << ")";
		}
	}
	return 0;
}

bool zhishu(int i)
{
	int k;
	bool flag=true;
	for (k=2;k<i;k++)
		if (i % k == 0)
		{
			flag = false;
			break;
		}	
	return flag;
}
```

## as6_3.cpp 
```C++
#include <iostream>
using namespace std;

bool zhishu(int i);

int main()
{
	int a=1,i;
	bool f;
	while ( a != 0)
	{
		f=true;
		a = 1;
		while (a % 2 !=0 || a <= 2)
		{
			cout << "请输入大于2偶数："; 
			cin >> a;		
		}
		for (i=2;i<=a/2;i++)
		{
			if (zhishu(i))
				if (zhishu(a-i))
					{
						cout << "对于输入的偶数，哥德巴赫猜想成立:" <<a<<"="<<i<<"+"<<a-i<<endl;
						f=false;
						break;
					}
		}
		if (f)
			cout <<"验证失败！"<<endl; 
	}
	return 0;
}

bool zhishu(int i)
{
	int k;
	bool flag=true;
	for (k=2;k<i/2;k++)
		if (i % k == 0)
		{
			flag = false;
			break;
		}	
	return flag;
}
```

## as7_1.cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	double i,s=0.0,t=-1.0;
	for (i=1.0;i<=100.0;i++)
	{
		t=-t;
		s+=t*1.0/i;
	}
	cout<<s;
	return 0;
}
```

## as7_2.cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	int a,b,c,m;
	cout << "请输入三个不同的正整数:" <<endl;
	cin >> a >> b >> c;
	if ((b<a&&a<c)||(c<a&&a<b))
		m = a;
	if ((a<b&&b<c)||(c<b&&b<a))
		m = b;
	if ((a<c&&c<b)||(b<c&&c<a))
		m = c;
	cout << "三个数中第二大的数是:" << m;
	return 0; 
}
```

## as7_3.cpp 
```C++
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
	int n,a,b,c,d,i;
	for (n=1100;n<=9988;n++)
	{
		a = n / 1000;
		b = n / 100 % 10;
		c = n % 100 / 10;
		d = n % 10;
		i = (int)sqrt(n);
		if (a==b && c==d && n==i*i)
		{
			cout << n;
			break;
		}
	}
	return 0;
}
```

## as8_1.cpp 
```C++
#include <iostream>
using namespace std;
#define N 100

int main()
{
	int i=0,j=0,t,p,r,imax;
	double s=0.0,max;
	int flag[N]={};
	char id[N][10],name[N][100];
	double score[N][9];
	while (cin)
	{
		cin>>id[i]; 		
		cin >> name[i];
		
		for (j=0;j<8;j++)
		{
			cin >> score[i][j];
			s += score[i][j];
		}
		score[i][8]=s/8;
		
		s=0.0;
		i += 1;
	}
	
	for (t=0;t<i-1;t++)
	{
		r=0;
		while (flag[r] == 1)
			r+=1;
		
		max=score[r][8];

		for (p=0;p<i;p++)
		{
			if (score[p][8] >= max && flag[p] == 0)
			{
				max=score[p][8];
				imax=p;
			}
		}
		flag[imax]=1;
		cout << id[imax] << " ";
		cout << name[imax] << " ";
		cout << score[imax][8] << endl;
	}
	return 0;
}
```

## as8_2.cpp 
```C++
#include <iostream>
using namespace std;
#define N 100

int main()
{
	int i=0,j,c=0,l=0,d=0;
	char a[N];
	int location[N][3];
	while(cin >> a[i])
	{
		if (a[i]>='A' && a[i]<='Z')
		{
			location[c][0] = i;
			c += 1;
		}
		
		if (a[i]>='a' && a[i]<='z')
		{
			location[l][1] = i;
			l += 1;
		}
		
		if (a[i]>='0' && a[i]<='9')
		{
			location[d][2] = i;
			d += 1;
		}
		i++;
	}
	
	cout << "Capital num: " << c <<": ";
	for (j=0;j<c;j++)
		cout << a[location[j][0]] <<" ";
	cout << endl;
	
	cout << "Lowercase num: " << l <<": ";
	for (j=0;j<l;j++)
		cout << a[location[j][1]] <<" ";
	cout << endl;
	
	cout << "Digits num: " << d <<": ";
	for (j=0;j<d;j++)
		cout << a[location[j][2]] <<" ";
	
	return 0;
}
```

## as9_1.cpp 
```C++
#include <iostream>
using namespace std;
#define N 100000

int mysort(int *p,int *q);
int main()
{
	int n,i,j,*p,*q,a[N];
	cout << "Please imput the number of int. :";
	cin >> n;
	cout <<"Please imput the numbers:"<<endl;
	for (i=0;i<n;i++)
		cin >> a[i];
	for (i=0;i<n;i++)
	{
		p=&a[i];
		for (j=i+1;j<n;j++)
		{
			q=&a[j];
			mysort(p,q);
		}
	}
	for (i=0;i<n;i++)
		cout << a[i] <<" ";
	return 0;
}

int mysort(int *p,int *q)
{
	int t;
	if (*p > *q)
	{
		t=*p;
		*p=*q;
		*q=t;
	}
}
```

## as9_2.cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	int *p=new int [10],n,i,count=0,max=10;
	cin >> n;
	while (n!=-1) //using -1 to stop the imput
	{
		p[count]=n;
		count++;
		if (count>=max)
		{
			max+=10;
			int *q=new int[max];
			for (i=0;i<count;i++)
				q[i]=p[i];
			delete []p;
			p = q;
		}
		cin >>n;
	}
	
	for (i=0;i<count;i++)
		cout << p[i] << " ";
	delete []p;
	return 0;
}
```

## test1_1.cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	int n,i,j,k,l;
	cout << "请输入一个正整数(0表示结束程序):";
	cin >> n;	
	while (n != 0)
	{
		for (i=0;i<=n;i++)
			for (j=0;j<=n;j++)
				for (k=0;k<=n;k++)
					for (l=0;l<=n;l++)
						if (n == i*i + j*j + k*k + l*l)
						{
							cout<<n<<"="<<i<<"*"<<i<<"+"<<j<<"*"<<j<<"+"<<k<<"*"<<k<<"+"<<l<<"*"<<l<<endl;
							goto End;
						}
		End:;			
		cout << "请输入一个正整数(0表示结束程序):";
		cin >> n;					
	}
	return 0;	
}
```

## test1_2.cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	int n,i,a1,a2,t;
	cout << "请输入一个台阶数(正整数，0表示结束程序):";
	cin >> n;	
	while (n !=0)
	{
		a1=1;a2=1;
		for (i=2;i<=n;i++)
		{
			t=a1+a2;
			a1=a2;
			a2=t;
		}
		cout << "跳法总数为:" << a2 << endl << "请输入一个台阶数(正整数，0表示结束程序):";	
		cin >> n;					
	}
	return 0;		
}
```

## test2_1.cpp 
```C++
#include <iostream>
using namespace std;

double e(int x);
int main()
{
	int x;
	cin >> x;
	cout << e(x);
	return 0;
}

double e(int x)
{
	if (x == 0) 
		return 1.0;
	else
	{
		int i=1,j;
		double sum=1.0,temp;
		do
		{
			temp = 1.0;
			for (j=1;j<=i;j++)
				temp = temp*double(x)/double(j);
			sum += temp;
			i += 1;
		}while (temp>=1e-7);
		return sum;
	}
}
```

## test2_2.cpp 
```C++
#include <iostream>
using namespace std;

int count(int n);
int main()
{
	int n;
	cin >> n;
	cout << count(n);
	return 0;
}

int count(int n)
{
	int i,j,k,s=1,t=1;
	if (n == 1)
		return 0;
	else if (n == 2)
		return 1;
	else
		return (n-1)*(count(n-1)+count(n-2));
		/* 前n-1封全装错 ，那么将第n封与之前任何一个交换，n个将全装错；
		前n-1个有一个装对，那么第n封只能和这一封交换 ；
		前n-1个有一个装对，相当于n-1(空闲位置数)乘以第n-1个装对，亦即前n-2个全部装错；*/ 
}
```

## test3_1.cpp 
```C++
#include <iostream>
#include <cstring>
using namespace std;

int strlen(const char *s[]);
int strncmp(const char *s1[],const char *s2[],int n);
int myfind(char s1[],const char s2[]);
int main()
{
	char s1[100],s2[50];
	cin >> s1 >> s2;
	cout << myfind(s1,s2);
	return 0;
} 

int myfind(char s1[],const char s2[])
{
	int i,j;
	bool flag=true;
	int l1=strlen(s1),l2=strlen(s2);
	for (i=0;i<=(l1-l2);i++)
		if (strncmp(s1+i,s2,l2)==0)
		{
			flag=false;
			return i;
		}
	if (flag) return -1;
}
```

## test3_2.cpp 
```C++
#include <iostream>
using namespace std;

struct node
{
	int content;
	node *next;
};
node *head=NULL;

node *mycreate(node *head);
node *mydelete(node *head);
void myprint(node *head);
void myfree(node *head);

int main()
{
	head=mycreate(head);
	//myprint(head);cout<<endl;
	head=mydelete(head);
	myprint(head);
	myfree(head);
}

node *mycreate(node *head)
{
	node *p=new node;
	head = p;
	p->next = NULL;
	cin >> p->content;
	node *q=p;
	while (p->content !=-1)
	{
		p=new node;
		cin >> p->content;
		q->next = p;
		p->next = NULL;
		q=p;
	}
	return head;
}

node *mydelete(node *head)
{
	node *h=head;
	while (h->content != -1)
	{
		node *p=h->next;
		while (p->content != -1)
			if (h->content == p->content)
			{ 
				h->next = p->next;
				node *q=p;
				p=p->next;
				delete q;
			} 
			else break;
		h = h->next;
	}
	return head;
}

void myprint(node *head)
{
	node *h=head;
	while (h->content !=-1)
	{
		cout << h->content <<" ";
		h = h->next;
	}
}

void myfree(node *head)
{
	while(head)
	{
		node *cur;
		cur = head;
		head = head->next;
		delete cur;
	}
}
```

阶乘的零(C).cpp 
```C++
#include<stdio.h>
int n,i,j,ans;

int main()
{
	while(scanf("%d",&n)!=EOF)
	{
		ans=0;
		for(i=5;i<=n;i*=5)
			for(j=1;j*i<=n;j++)
				ans++;
		printf("%d\n",ans);
	}
	return 0;
}
```

阶乘的零(C++).cpp 
```C++
#include <iostream>
using namespace std;

int main()
{
	int n,i,j,k;
	while(cin >> n)
	{
		k=0;
		for (i=1;i<=n;i++)
		{
			j=i;
			while(j%5==0 && j!=0)
			{
				k++;
				j= j / 5;
			}
		}
		cout << k <<endl;
	}
	return 0;
}
```
