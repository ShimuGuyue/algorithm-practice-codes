

```cpp
void solve()
{
    int n;
    std::cin >> n;
    std::vector<std::pair<int, int>> abs(n);
    for (auto& [a, b] : abs)
    {
        std::cin >> a >> b;
    }
    int m;
    std::cin >> m;
    std::vector<std::string> ss(m);
    for (auto& s : ss)
    {
        std::cin >> s;
    }

    std::vector<std::vector<bool>> flags(10 + 1, std::vector<bool>('z' + 1));
    for (int i{ 0 }; i < n; ++i)
    {
        auto [a, b]{ abs[i] };
        for (auto& s : ss)
        {
            if (s.length() != a)
                continue;
            flags[i][s[b - 1]] = true;
        }
    }

    for (std::string s : ss)
    {
        if (s.length() != n)
        {
            std::cout << "No\n";
            continue;
        }
        bool ok{ true };
        for (int i{ 0 }; i < n; ++i)
        {
            if (!flags[i][s[i]])
            {
                ok = false;
                break;
            }
        }
        std::cout << (ok ? "Yes\n" : "No\n");
    }
}
```

