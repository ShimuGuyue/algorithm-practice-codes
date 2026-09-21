

```c++
void solve()
{
    std::array<int, 3> as;
    for (auto& a : as)
    {
        std::cin >> a;
    }

    std::sort(as.begin(), as.end());
    if (as[2] - as[0] > 1)
        std::cout << "NO\n";
    else
        std::cout << "YES\n";
}
```

