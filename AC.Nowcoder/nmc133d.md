

```cpp
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    if (*std::max_element(as.begin(), as.end()) == 1)
    {
        std::cout << -1 << '\n';
        return;
    }

    std::vector<int> flags(100000 + 1);
    for (auto a : as)
    {
        int flag{ 2 };
        while (a > 1)
        {
            if (a % flag == 0)
                ++flags[flag];
            while (a % flag == 0)
            {
                a /= flag;
            }
            ++flag;
        }
    }

    int max{ *std::max_element(flags.begin(), flags.end()) };
    int ans{ n - max };
    std::cout << ans << '\n';
}
```

