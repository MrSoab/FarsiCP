---
layout: Wiki
---

# الگوریتم بلمن فورد
پیدا کردن کوتاه ترین مسیر از یک مبدا مشخص و داشتن دور منفی در گراف :
فرض کنید گراف وزن دار و جهت داری با $n$ راس و $m$ یال داریم و می خواهیم کوتاه ترین مسیر از راس مشخص $s$ را به بقیه رئوس پیذا کنیم . یکی از مزیت های این الگوریتم نسبت به [دایکسترا] ، توانایی اجرا شدن آن روی گراف ها با یال منفی است . با این وجود ، اگر گراف شامل دور منفی باشد(یعنی مجموع وزن یال های دور منفی باشد)آنگاه واضح است که ممکن است کوتاه ترین مسیر به بعضی از راس ها وجود نداشته باشد . با توجه به این $fact$ که کوتاه ترین مسیر منفی بی نهایت است . با این وجود ، این الگوریتم می تواند دور منفی را شناسایی کرده و در روندش تغییر کند . 

# توضیح 
در ابتدا بیاید فرض کنیم گراف هیچ درو منفی ندارد . در قسمت بعدی راجع به وجود دور منفی توضیحاتی داده شده است . یک آرایه $d[]$ که شامل طول کوتاه ترین مسیر فعلی است و بعد از اجرای کامل این الگوریتم این مقدار کمترین است و در مقدار دهی اولیه $d[s] = 0$ است و برای هر راس دیگری مانند $v$ ، $d[v]$ بی نهایت است . در پیاده سازی منظور از بی نهایت ، عدد بزرگی است که تضمین می شود طول همه کوتاه ترین ها از آن کمتر است . 
این الگوریتم شامل تعدادی مرحله است و در هر مرحله همه یال های گراف امتحان می شود تا عملیت $relaxation$ در طول یالی مانند $(v , u)$ با وزن $w$ اتفاق بیفتد . در واقع این عملیات سعی می کند تا مقدار $d[u]$ را با استفاده از $d[v] + w$ بهتر و کمتر بکند . این بدان معنا  است که ما سعی می کنیم جواب(طول کوتاه ترین مسیر) را برای این راس با استفاده از یال $(v , u)$ بهتر کنیم :
$relax d[u] : d[u] = min(d[u] , d[v] + w)$
ادعا می کنیم که $n - 1$ مرحله کافی است تا ما جواب درست را برای هر راس پیدا کنیم . دقت کنید که همچنان فرض کرده ایم که گراف مان دور منفی ندارد و توجه داشته باشید که اگر از راس $s$ نتوان به راس $v$ رسید ، مثلا اگر این دو راس در مولفه های متفاوت بودند ، آنگاه $d[v]$ همان بی نهایت باقی می ماند . 

# اثبات 
درستی این الگوریتم را با استقرا ثابت می کنیم . فرض کنید این اگوریتم تا مرحله $i$ام کوتاه ترین فاصله تمام رئوسی که کم وزن ترین مسیر آن ها حداکثر $i$ یال دارد را به درستی پیدا کرده است . پایه اسستقرا : در مرحله صفرام راس آغاز فاصله اش صفر است ، پس درست است . گام استقرا : هر یک از راس هایی که کوتاه ترین مسیر شان حداکثر $i + 1$ یال دارد آخرین بال شان حتما به یک راسی است که در مرحله قبلی فاصله شان پیدا شده است (راس هایی که کوتاه ترین مسیرشان حداکثر $i$ یال دارد) پس بعد از $relax$ کردن یال ها برای بار $i + 1$ام جواب تمام راس هایی که کوتاه تریم مسیرشان $i + 1$ یالی است را پیدا کرده ایم . پس درستی الگوریتم ثابت می شود . آخرین چیزی که باید به آن توجه داشت این است که هیچ کوتاه ترین مسیری نمی تواند بیشتر از $n - 1$ یال داشته باشد . بنابراین الگوریتم بعد ار $n - 1$ مرحله به پایان می رسد و بعد از این تعداد هیچ تضمینی وجود ندارد که مقدار $d[]$ را برای رئوس بهتر کند . 

# وجود دور منفی 
در قسمت های بالایی فرض کردیم که هیچ دور منفی در گراف وجود ندارد . دقت کنید که دور های منفی برای ما مهم هستند که از راس $s$ بتوان به آن ها رسید و اگر دور منفی باشد که نتوان به آن رسید ، آنگاه هیچ تغییری در توضیحات بالا رخ نمی دهد . این واضح است که الگوریتم بلمن فورد می تواند عملیات $relax$ کردن را برای راس های دور منفی و راس هایی که می توان از $s$ به آن ها رسید را بی نهایت بار انجام می دهد . بنابراین اگر ما برای تکرار این عملیات $limit$ نگذاریم $(n - 1)$ آنگاه این عملیات به صورت نامحدودی ادامه می یابد . اگر بعد از $n - 1$ مرحله ، ما یک مرحله دیگر الگوریتم را اجرا کنیم و و حداقل یک عملیات $relax$ کردن دیگر اتفاق افتاد ، آنگاه گراف شامل دور منفی است که می توان از $s$ به آن رسید و اگر نه ، همچین دوری وجود ندارد . پس بدین صورت می توان متوجه وجود دور منفی در گراف شد . به علاوه اگر چنین دوری در گراف بود آنگاه این الگوریتم می تواند طور دیگری عمل کند و این دور را به عنوان رشته ایی از رئوس در نظر بگیرد . برای همین کافی است که آخرین راسی که در مرحله $n$ام ، $relax$ می شود را ذخیره کنیم . فرض می کنیم این راس $x$ باشد پس راس $x$ یا یکی از راس های دور منفی است یا از طریق یک دور منفی می توان به آن رسید . برای به دست آوردن را راس هایی که در دور منفی هستند باید از $x$ شروع کرد و $n$ بار به جد آن رفت . فرض کنید بعد ازاین کار به راس $y$ می رسیم . درواقع راس $y$ اولین راس در دور منفی است که می توان به آن رسید و حتما این اتفاق می افتد چون عملیات $relax$ کردن رئوس دور به صورت دایره ایی اتفاق می افتد . 

# پیاده سازی 
برای تشخیص دور منفی و رئوس آن داریم :

```C++
void solve()
{
    vector<int> d (n, INF);
    d[v] = 0;
    vector<int> p (n - 1);
    int x;
    for (int i=0; i<n; ++i)
    {
        x = -1;
        for (int j=0; j<m; ++j)
            if (d[e[j].a] < INF)
                if (d[e[j].b] > d[e[j].a] + e[j].cost)
                {
                    d[e[j].b] = max (-INF, d[e[j].a] + e[j].cost);
                    p[e[j].b] = e[j].a;
                    x = e[j].b;
                }
    }

    if (x == -1)
        cout << "No negative cycle from " << v;
    else
    {
        int y = x;
        for (int i=0; i<n; ++i)
            y = p[y];

        vector<int> path;
        for (int cur=y; ; cur=p[cur])
        {
            path.push_back (cur);
            if (cur == y && path.size() > 1)
                break;
        }
        reverse (path.begin(), path.end());

        cout << "Negative cycle: ";
        for (size_t i=0; i<path.size(); ++i)
            cout << path[i] << ' ';
    }
}
```
برای پیدا کردن کوتاه ترین مسیر ها از راس $s$ داریم :

```C++
#include <iostream>
#include <vector>
 
using namespace std;
 
typedef pair<int, int> pii;
const int MAXN = 1e5 + 10;
const int INF = 1e9;
int dist[MAXN];
vector<pii> edge;
vector<int> w;
int n, m;
 
void readInput()
{
	cin >> n >> m;
	for(int i=0; i<m; ++i)
    {
		int u, v, z;
		cin >> u >> v >> z;
		edge.push_back(pii(u, v));
		w.push_back(z);
	}
}
 
void bellmanFord(int s)
{
	dist[s] = 0;
	for(int i=0; i<n; ++i)
		if(i!=s)
			dist[i] = INF;
	for(int i=0; i<n-1; ++i)
		for(int j=0; j<(int)edge.size(); ++j){
			int u = edge[j].first;
			int v = edge[j].second;
			dist[v] = min(dist[v], dist[u]+w[j]);
		}
}
 
void writeOutput()
{
	for(int i=0; i<n; ++i)
		cout << dist[i] << " ";
	cout << endl;
}
 
int main()
{
	readInput();
	bellmanFord(0);
	writeOutput();
	return 0;
}
```
دقت کنید که این پیاده سازی در $Order(n * n)$ انجام می شود . هر چند می توان با استفاده از داده ساختار هرم پیاده سازی از $O(m * Log(n))$ ارائه داد .

# مسائل تمرینی
*[E-OLIMP #1453 "Ford-Bellman"](http://www.e-olimp.com.ua/problems/1453)
*[UVA #423 "MPI Maelstrom"](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=364)
*[UVA #534 "Frogger"](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&category=7&page=show_problem&problem=475)
*[UVA #10099 "The Tourist Guide"](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&category=12&page=show_problem&problem=1040)
*[UVA #515 "King"](https://uva.onlinejudge.org/index.php?option=onlinejudge&page=show_problem&problem=456)
*[UVA 12519 - The Farnsworth Parabox](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=3964)

[دایکسترا]:Dijkstra