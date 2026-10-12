

```cpp
void solve()
{
    int n, k;
    std::cin >> n >> k;
    std::string s;
    std::cin >> s;

    if (n < 17)
    {
        std::cout << "No\n";
        return;
    }

    s = " " + s;

    std::string a{ "awdec" };
    std::string b{ "Fantasy_Blue" };
    std::vector<int> difs(n + 1);
    for (int i{ 1 }; i + 4 <= n; ++i)
    {
        for (int j{ 0 }; j <= 4; ++j)
        {
            difs[i] += (a[j] != s[i + j]);
        }
    }
    std::vector<int> premins(n + 2, n);
    std::vector<int> sufmins(n + 2, n);
    for (int i{ 1 }; i + 4 <= n; ++i)
    {
        premins[i] = std::min(premins[i - 1], difs[i]);
    }
    for (int i{ n - 4 }; i > 0; --i)
    {
        sufmins[i] = std::min(sufmins[i + 1], difs[i]);
    }

    int ans{ n };
    for (int i{ 1 }; i + 11 <= n; ++i)
    {
        int dif{ 0 };
        for (int j{ 0 }; j <= 11; ++j)
        {
            dif += (b[j] != s[i + j]);
        }
        int min{ n };
        if (i - 5 >= 1)
            min = std::min(min, premins[i - 5]);
        if (i + 16 <= n)
            min = std::min(min, sufmins[i + 12]);
        ans = std::min(ans, dif + min);
    }
    std::cout << (ans <= k ? "Yes" : "No") << '\n';
}
```

