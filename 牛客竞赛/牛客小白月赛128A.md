

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::string s;
    std::cin >> s;
    std::string t;
    std::cin >> t;

    for (char& c : s)
    {
        if (c == 'O')
            c = '0';
        if (c == 'I' || c == 'l')
            c = '1';
    }
    for (char& c : t)
    {
        if (c == 'O')
            c = '0';
        if (c == 'I' || c == 'l')
            c = '1';
    }
    if (s == t)
        std::cout << "yes\n";
    else
        std::cout << "no\n";
}
```

