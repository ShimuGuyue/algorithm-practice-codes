

```cpp
void solve()
{
    int a, b;
    std::cin >> a >> b;

    int g{ std::gcd(a, b) };
    std::vector<int> factors;
    for (int i{ 1 }; i * i <= g; ++i)
    {
        if (g % i)
            continue;
        factors.push_back(i);
        if (i * i != g)
            factors.push_back(g / i);
    }
    std::sort(factors.begin(), factors.end());

    int q;
    std::cin >> q;
    while (q--)
    {
        int l, r;
        std::cin >> l >> r;
        auto it{ std::prev(std::upper_bound(factors.begin(), factors.end(), r)) };
        if (*it >= l)
            std::cout << *it << '\n';
        else
            std::cout << -1 << '\n';
    }
}
```

