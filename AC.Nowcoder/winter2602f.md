

```c++
void solve()
{
    int64_t n;
    std::cin >> n;

    int bit{ calc(n) };

    int64_t ans1{ n << bit };
    int64_t ans2{ ans1 | n };
    std::cout << ans1 << ' ' << ans2 << '\n';
}

int calc(int n)
{
    int ans{ 0 };
    while (n)
    {
        n /= 2;
        ++ans;
    }
    return ans;
}
```

