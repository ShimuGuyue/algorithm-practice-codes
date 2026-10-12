

```c++
void solve()
{
    int n, m, k;
    std::cin >> n >> m >> k;
    std::map<int, int> digits;
    for (int i = 0; i < n * m; ++i)
    {
        int a;
        std::cin >> a;
        if (a)
            ++digits[a];
    }

    int ans1{ 0 }, ans2{ 0 };
    while (!digits.empty())
    {
        auto [u, v]{ *digits.begin() };
        ans1 += v / 2;
        if (u + 1 >= k)
            ans2 += v / 2;
        if (v / 2)
            digits[u + 1] += v / 2;
        digits.erase(u);
    }
    std::cout << ans1 << ' ' << ans2 << '\n';
}
```

