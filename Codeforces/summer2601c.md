

```cpp
struct DisjointSet
{
    struct Data
    {
        int father;
        int size;
        int weight;
        int dist;
    };
    std::vector<Data> datas;

    DisjointSet(int n) : datas(n)
    {
        for (int i{ 0 }; i < n; ++i)
        {
            datas[i].father = i;
            datas[i].size = 1;
            datas[i].weight = 0;
            datas[i].dist = 0;
        }
    }

    int find(int x)
    {
        if (datas[x].father == x)
            return x;
        int root{ find(datas[x].father) };
        datas[x].dist = std::max(datas[x].dist, datas[datas[x].father].dist);
        datas[x].father = root;
        return root;
    }

    void merge(int x, int y)
    {
        datas[x].father = y;
        datas[x].dist = datas[y].weight - datas[x].size + 1;
        datas[y].size += datas[x].size;
    }
};
```

```cpp
void solve()
{
    int n, m, q;
    std::cin >> n >> m >> q;

    DisjointSet ds((n + 1) * (m + 1) + 1);

    auto turn = [m](int x, int y) -> int
    {
        return x * (m + 1) + y;
    };

    std::array<std::pair<int, int>, 4> dxys = { std::pair<int, int>
        { -1, 0 }, { 0, -1 }, { 0, 1 }, { 1, 0 }
    };

    int ans{ 0 };
    while (q--)
    {
        int op;
        std::cin >> op;
        if (op == 1)
        {
            int x, y, v;
            std::cin >> x >> y >> v;
            x ^= ans; y ^= ans;
            ds.datas[turn(x, y)].weight = v;
            for (auto [dx, dy] : dxys)
            {
                int xx{ x + dx };
                int yy{ y + dy };
                if (xx == 0 || xx > n)
                    continue;
                if (yy == 0 || yy > m)
                    continue;
                int p{ turn(xx, yy) };
                if (ds.datas[p].weight == 0)
                    continue;
                int root{ ds.find(p) };
                if (root == turn(x, y))
                    continue;
                ds.merge(root, turn(x, y));
            }
            ans = ds.datas[ds.find(turn(x, y))].size - 1;
        }
        else
        {
            int x, y;
            std::cin >> x >> y;
            x ^= ans; y ^= ans;
            int p{ turn(x, y) };
            ds.find(p);
            ans = std::max(0, ds.datas[p].dist - ds.datas[p].weight);
        }
        std::cout << ans << '\n';
    }
}
```

