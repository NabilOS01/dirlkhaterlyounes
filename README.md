# dirlkhaterlyounes

app.get('/health', async (req, res) => {
    try {
        const health = await client.cluster.health();
        res.json({ status: 'Elasticsearch is reachable', health });
    } catch (error) {
        console.error('Elasticsearch cluster is not reachable', error);
        res.status(500).json({ status: 'Elasticsearch is not reachable', error: error.message });
    }
});
