

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    std::vector<int> ls(n);
    std::vector<int> rs(n);
    int flag;
    flag = as.front() + 1;
    ls.front() = as.front();
    for (int i = 1; i < n; ++i)
    {
        if (as[i] <= flag)
            flag = as[i];
        ls[i] = flag;
        ++flag;
    }
    flag = as.back() + 1;
    rs.back() = as.back();
    for (int i = n - 2; i >= 0; --i)
    {
        if (as[i] <= flag)
            flag = as[i];
        rs[i] = flag;
        ++flag;
    }

    int64_t ans{ 0 };
    for (int i = 0; i < n; ++i)
    {
        ans += std::abs(std::min(ls[i], rs[i]) - as[i]);
    }
    std::cout << ans << '\n';
}
```

