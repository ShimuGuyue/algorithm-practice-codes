

```c++
void solve()
{
    int n, h;
    std::cin >> n >> h;
    std::vector<int> ts(n);
    std::vector<int> ls(n);
    std::vector<int> rs(n);
    for (int i = 0; i < n; ++i)
    {
        std::cin >> ts[i] >> ls[i] >> rs[i];
    }

    int t{ 0 };
    int l{ h };
    int r{ h };
    for (int i = 0; i < n; ++i)
    {
        int dif = ts[i] - t;
        t = ts[i];
        l = std::max(ls[i], l - dif);
        r = std::min(rs[i], r + dif);
        if (l > r)
        {
            std::cout << "No\n";
            return;
        }
    }
    std::cout << "Yes\n";
}
```

