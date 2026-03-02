

```c++
void solve()
{
    int64_t n, q;
    std::cin >> n >> q;
    while (q--)
    {
        int64_t x;
        std::cin >> x;
        if (count_bit(x) != count_bit(n))
            std::cout << (INT64_C(1) << (count_bit(x) - 1)) << '\n';
        else
            std::cout << n - ((INT64_C(1) << (count_bit(x) - 1)) - 1) << '\n';
    }
}

int count_bit(int64_t x)
{
    int ans{ 0 };
    while (x)
    {
        ++ans;
        x /= 2;
    }
    return ans;
}
```

