

```c++
void solve()
{
    int a, b, c;
    std::cin >> a >> b >> c;
    if (a + b == c)
    {
        std::cout << "YES\n";
        return;
    }
    if (a - b == c)
    {
        std::cout << "YES\n";
        return;
    }
    if (a * b == c)
    {
        std::cout << "YES\n";
        return;
    }
    if (a % b == 0 && a / b == c)
    {
        std::cout << "YES\n";
        return;
    }
    std::cout << "NO\n";
}
```

