

```c++
void solve()
{
    std::string s;
    std::cin >> s;

    int64_t ans{ 1 };
    int same{ 0 }, unsame{ 0 };
    for (int i{ 1 }; i < s.length(); ++i)
    {
        if (s[i - 1] == s[i])
        {
            ans += unsame;
            ++same;
        }
        else
        {
            ans += same;
            ++unsame;
        }
    }

    std::cout << ans << '\n';
}
```

