

```c++
void solve()
{
    std::string s;
    std::cin >> s;

    int n{ int(s.length()) };
    s += "-";

    int r{ n - 1 };
    for (int i = 0; i < r; ++i)
    {
        if (s[i] != '0')
            continue;
        int l{ i - 1 };
        while (l >= 0 && s[l] == '1')
        {
            while (r > i && s[r] != '1')
            {
                --r;
            }
            if (s[r] == '1')
            {
                s[l] = '-';
                s[r] = '2';
            }
            else
            {
                break;
            }
            --l;
        }
    }

    for (char c : s)
    {
        if (c != '-')
            std::cout << c;
    }
    std::cout << '\n';
}
```

