

```c++
void solve()
{
    double x1, y1, x2, y2;
    std::cin >> x1 >> y1 >> x2 >> y2;

    auto calc = [x1, y1, x2, y2](double x3, double y3 = 0)
    {
        return fabs(x1 * (y2 - y3) + x2 * (y3 - y1) + x3 * (y1 - y2));
    };

    if (y1 == y2)
    {
        double s{ calc(0) };
        if (fabs(s - 4) < 1e-9)
            std::cout << 0 << '\n';
        else
            std::cout << "no answer\n";
        return;
    }

    if (x1 == x2)
    {
        double a{ fabs(y1 - y2) };
        double h{ 4 / a };
        std::cout << x1 + h << '\n';
        return;
    }

    // y1 = k * x1 + b
    // y2 = k * x2 + b
    //      (y1 - y2) = k * (x1 - x2)
    //      k = (y1 - y2) / (x1 - x2)
    //      b = y1 - k * x1
    double k{ (y1 - y2) / (x1 - x2) };
    double b{ y1 - k * x1 };
    // 0 = k * x + b
    //      x = -b / k
    double x{ -b / k };

    double l{ x }, r{ 1e18 };
    while (r - l > 1e-9)
    {
        double mid{ (l + r) / 2 };
        if (calc(mid) < 4)
            l = mid;
        else
            r = mid;
    }
    std::cout << std::fixed << std::setprecision(10) << (l + r) / 2 << '\n';
}
```

