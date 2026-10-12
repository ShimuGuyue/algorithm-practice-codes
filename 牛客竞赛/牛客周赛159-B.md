

```cpp
void solve()
{
    int64_t x;
    std::cin >> x;
    if (x == 0)
    {
        std::cout << "0 -1 -1\n";
        return;
    }

    std::cout << std::popcount(uint64_t(x)) << ' ';
    for (int i{ 0 }; i <= 60; ++i)
    {
        if (x >> i & 1)
        {
            std::cout << i << ' ';
            break;
        }
    }
    for (int i{ 60 }; i >= 0; --i)
    {
        if (x >> i & 1)
        {
            std::cout << i << '\n';
            break;
        }
    }
}
```

