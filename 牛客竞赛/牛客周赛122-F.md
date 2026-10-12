

```c++
class ST
{
private:
    std::vector<std::vector<int>> st;

    std::vector<int> v_;

public:
    ST()
    {}

    ST(const std::vector<int> &v)
    {
        build(v);
    }

private:
    int merge(int ia, int ib)
    {
        if (v_[ia] > v_[ib])
            return ia;
        if (v_[ia] < v_[ib])
            return ib;
        return std::min(ia, ib);
    }

public:
    void build(const std::vector<int> &v)
    {
        v_ = v;

        int n = v.size();
        int m = log2(n) + 1;
        st.assign(n, std::vector<int>(m));

        for (int i = 0; i < n; ++i)
        {
            st[i][0] = i;
        }
        for (int j = 1; j < m; ++j)
        {
            int len = 1 << (j - 1);
            for (int i = 0; i < n - (1 << j) + 1; ++i)
            {
                st[i][j] = merge(st[i][j - 1], st[i + len][j - 1]);
            }
        }
    }

    int query(int l, int r)
    {
        int power = log2(r - l + 1);
        int len = 1 << power;
        return merge(st[l][power], st[r - len + 1][power]);
    }
};
```

```c++
void solve()
{
    int n, k;
    std::cin >> n >> k;
    std::vector<int> as(n);
    for (auto &a : as)
    {
        std::cin >> a;
    }

    ST st(as);

    for (int i = 0; i < n - 1; ++i)
    {
        if (k <= 0)
            break;
        int l{ i + 1 };
        int r{ i + k < n ? i + k : n - 1 };
        if (l > r)
            break;
        r = st.query(l, r);
        if (as[r] > as[i])
        {
            for (int j = i; j < r; ++j)
            {
                as[j] = as[r];
                --k;
            }
            i = r - 1;
        }
        else
        {
            if (i + k + 1 < n)
            {
                if (as[i] >= as[i + k + 1])
                {
                    if (as[i] > as[i + 1])
                    {
                        as[i + 1] = as[i];
                        --k;
                    }
                }
                else
                {
                    if (as[i + k + 1] > as[i + 1])
                    {
                        int k_{ k };
                        for (int j = i + 1; j < i + k_ + 1; ++j)
                        {
                            as[j] = as[i + k_ + 1];
                            --k;
                        }
                        i = i + 1 + k_;
                    }
                }
            }
            else
            {
                if (as[i] > as[i + 1])
                {
                    as[i + 1] = as[i];
                    --k;
                }
            }
        }
    }

    for (auto a : as)
    {
        std::cout << a << ' ';
    }
    std::cout << '\n';
}
```

