

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::map<int, int> m;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
        ++m[a];
    }

    auto [max, count]{ *m.rbegin() };

    for (auto a : as)
    {
        if (a == max)
        {
            if (count & 1)
                std::cout << 1;
            else
                std::cout << 0;
        }
        else
        {
            if (count & 1)
                std::cout << 0;
            else
                std::cout << 1;
        }
    }
    std::cout << '\n';
}
```

