

```cpp
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }
    int x;
    std::cin >> x;
    std::cout << as[x - 1] << '\n';
}
```

