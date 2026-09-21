

```cpp
void solve()
{
    static std::set<int> as{ 'a', 'e', 'i', 'o', 'u' };

    std::string s;
    std::cin >> s;

    if (s.length() != 8)
    {
        std::cout << "Well-Being\n";
        return;
    }

    for (int i{ 0 }; i < 8; ++i)
    {
        if (i % 2 == 0 && as.count(s[i]))
        {
            std::cout << "Well-Being\n";
            return;
        }
        if (i % 2 == 1 && !as.count(s[i]))
        {
            std::cout << "Well-Being\n";
            return;
        }
    }
    std::cout << "Suspected Virus\n";
}
```

