

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    for (auto& a : as)
    {
        if (a <= (n + 1) / 2)
            a = ((n + 1) / 2 + 1) / 2;
    }
    for (auto a : as)
    {
        std::cout << a << ' ';
    }
    std::cout << '\n';
}
```

