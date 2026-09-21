

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::cin >> as[i];
    }

    std::sort(as.begin(), as.end());

    int ans{ 0 };
    int count{ 1 };
    for (int i = 1; i <= n; ++i)
    {
        if (i != n && as[i] == as[i + 1])
        {
            ++count;
            continue;
        }
        if (i - 1 >= (n - i) * 4)
            ans += as[i] * count;
        count = 1;
    }
    std::cout << ans << '\n';
}
```

