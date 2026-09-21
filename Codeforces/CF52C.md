

```cpp
struct SegmentTree
{
    struct Data
    {
        int seg_l, seg_r;
        int64_t tag{ 0 };
        int64_t data{ 0 };
    };

    std::vector<int64_t>& v;
    std::vector<Data> tree;

    SegmentTree(std::vector<int64_t>& v) : v(v)
    {
        tree.assign(v.size() * 4, { });
        build(0, 0, v.size() - 1);
    }

    void build(int node, int l, int r)
    {
        tree[node].seg_l = l;
        tree[node].seg_r = r;
        if (l == r)
        {
            tree[node].data = v[l];
            return;
        }
        int mid{ (l + r) / 2 };
        build(node * 2 + 1, l, mid);
        build(node * 2 + 2, mid + 1, r);
        pushup(node);
    }

    void update(int l, int r, int64_t data, int node = 0)
    {
        auto& [seg_l, seg_r, tag, d]{ tree[node] };
        if (l == seg_l && r == seg_r)
        {
            tag += data;
            d += data;
            return;
        }
        pushdown(node);
        int mid{ (seg_l + seg_r) / 2 };
        if (r <= mid)
            update(l, r, data, node * 2 + 1);
        else if (l > mid)
            update(l, r, data, node * 2 + 2);
        else
            update(l, mid, data, node * 2 + 1),
            update(mid + 1, r, data, node * 2 + 2);
        pushup(node);
    }

    int64_t query(int l, int r, int node = 0)
    {
        auto& [seg_l, seg_r, tag, data]{ tree[node] };
        if (l == seg_l && r == seg_r)
            return data;
        pushdown(node);
        int mid{ (seg_l + seg_r) / 2 };
        if (r <= mid)
            return query(l, r, node * 2 + 1);
        else if (l > mid)
            return query(l, r, node * 2 + 2);
        else
            return std::min(query(l, mid, node * 2 + 1), query(mid + 1, r, node * 2 + 2));
    }

    void pushup(int node)
    {
        int node_l{ node * 2 + 1 };
        int node_r{ node * 2 + 2 };
        tree[node].data = std::min(tree[node_l].data, tree[node_r].data);
    }

    void pushdown(int node)
    {
        for (int i : {1, 2})
        {
            int child{ node * 2 + i };
            auto& [seg_l, seg_r, tag, data]{ tree[child] };
            tag += tree[node].tag;
            data += tree[node].tag;
        }
        tree[node].tag = 0;
    }
};
```

```cpp
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int64_t> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    SegmentTree st(as);

    int m;
    std::cin >> m;
    std::cin.ignore();
    while (m--)
    {
        std::string s;
        std::getline(std::cin, s);
        s += " ";
        static constexpr int64_t inf{ std::numeric_limits<int>::max() };
        int64_t l{ inf }, r{ inf }, x{ inf };
        std::string temp;
        for (char c : s)
        {
            if (c == ' ')
            {
                if (l == inf)
                    l = std::stoll(temp);
                else if (r == inf)
                    r = std::stoll(temp);
                else
                    x = std::stoll(temp);
                temp.clear();
            }
            else
            {
                temp += c;
            }
        }

        if (x == inf)
        {
            if (r >= l)
                std::cout << st.query(l, r) << '\n';
            else
                std::cout << std::min(st.query(0, r), st.query(l, n - 1)) << '\n';
        }
        else
        {
            if (r >= l)
                st.update(l, r, x);
            else
                st.update(0, r, x),
                st.update(l, n - 1, x);
        }
    }
}
```

