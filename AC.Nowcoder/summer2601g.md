

```cpp
void solve()
{
    int n;
    std::cin >> n;

    std::cout << n * 2 << '\n';
    std::cout << std::fixed << std::setprecision(10);
    double x1{ 0 }, x2{ 1 };
    for (double y{ 0 }; y < 10; ++y)
    {
        for (double z{ 0 };z < 10; ++z)
        {
            std::cout << x1 << ' ' << y * 0.01001 << ' ' << z * 0.01001 << '\n';
            std::cout << x2 << ' ' << y * 0.01001 << ' ' << z * 0.01001 << '\n';
            --n;
            if (n == 0)
                return;
        }
    }
}
```

