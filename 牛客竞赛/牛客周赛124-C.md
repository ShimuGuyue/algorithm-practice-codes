

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    std::sort(as.begin(), as.end());

    as.push_back(0);

    int flag{ -1 };
    int len{ 0 };
    std::vector<std::pair<int, int>> flags;
    for (auto a : as)
    {
        if (a == flag + 1)
        {
            flag = a;
            ++len;
        }
        else
        {
            if (len != 0)
                flags.push_back({flag - len + 1, len});
            flag = a;
            len = 1;
        }
    }
    for (int i = 0; i < flags.size(); ++i)
    {
        auto [l, len_l]{ flags[i] };

        if (len_l + 1 == m)
        {
            std::cout << "YES\n";
            return;
        }
    }
    for (int i = 1; i < flags.size(); ++i)
    {
        auto [l, len_l]{ flags[i - 1] };
        auto [r, len_r]{ flags[i] };

        if (l + len_l + 1 == r && len_l + len_r + 1 >= m)
        {
            std::cout << "YES\n";
            return;
        }
    }
    std::cout << "NO\n";
}
```

