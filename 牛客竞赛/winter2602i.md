

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<std::string> vs(n);
    for (auto& s : vs)
    {
        std::cin >> s;
    }

    int count0{ 0 }, count1{ 0 };
    for (auto& s : vs)
    {
        for (char c : s)
        {
            if (c == '1')
                ++count1;
            else
                ++count0;
        }
    }

    for (auto& s : vs)
    {
        for (char c : s)
        {
            if (c == '1')
                if (count1 > 1)
                    std::cout << "Y";
                else
                    std::cout << "N";
            else
                if (count0 > 1)
                    std::cout << "Y";
                else
                    std::cout << "N";
        }
        std::cout << '\n';
    }
}
```

