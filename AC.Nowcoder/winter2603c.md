

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::string s;
    std::cin >> s;
    int ans{ std::min(calc(s, '0'), calc(s, '1')) };
    std::cout << ans << '\n';
}

int calc(std::string s, char c)
{
    int n{ int(s.length()) };
    std::vector<char> flags;
    for (int i = 0; i < n; ++i)
    {
        if (i & 1)
        {
            if (s[i] == c)
                flags.push_back(s[i]);
        }
        else
        {
            if (s[i] != c)
                flags.push_back(s[i]);
        }
    }

    int count0{ 0 };
    int count1{ 0 };
    for (char c : flags)
    {
        if (c == '1')
        {
            if (count0)
                --count0;
            ++count1;
        }
        else
        {
            if (count1)
                --count1;
            ++count0;
        }
    }

    int ans{ count0 + count1 };
    return ans;
}
```

