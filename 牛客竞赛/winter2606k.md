

```c++
void solve()
{
    int64_t n, m, z;
    std::cin >> n >> m >> z;
    z %= (n + m);
    if (z == 0)
    {
        std::cout << 1;
        return;
    }
    if (z <= n)
    {
        std::cout << 0;
    }
    else
    {
        std::cout << 1;
    }
}
```

