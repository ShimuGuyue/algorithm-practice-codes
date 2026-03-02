

```c++
void solve()
{
    std::string s;
    std::cin >> s;

    int n{ int(s.length()) };
    for (int i = 0; i < n; ++i)
    {
        if (s[i] < '5')
            continue;
        if (i == 0)
        {
            std::cout << 1;
            for (int j = 0; j < n; ++j)
            {
                std::cout << 0;
            }
            std::cout << '\n';
            return;
        }
        else
        {
            ++s[i - 1];
            for (int j = i; j < n; ++j)
            {
                s[j] = '0';
            }
            std::cout << s << '\n';
            return;
        }
    }

    s.back() = '0';
    std::cout << s << '\n';
}
```

