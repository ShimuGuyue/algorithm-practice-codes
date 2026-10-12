

```c++
void solve()
{
    int n, k;
    std::cin >> n >> k;
    std::string s;
    std::cin >> s;

    std::vector<int> ans(n + 1);
    int x{ 0 };
    int count{ 0 };
    for (int i = 0; i < n; ++i)
    {
        if (s[i] == '1')
            count = 0;
        else
            ++count;

        if (count == k)
        {
            ans[x] = i;
            ans[x + 1] = i + 1;
            ++x;
            count = 0;
        }
    }
    if (count < k)
        ans[x] = n;
    while (x <= n)
    {
        ans[x] = std::max(ans[x], ans[x - 1]);
        ++x;
    }
    for (auto a : ans)
    {
        std::cout << a << ' ';
    }
    std::cout << '\n';
}
```

