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

 fetch('/health')
.then(response => response.json())
.then(data => {
    const healthStatus = document.getElementById('health-status');
    if (data.status === 'Elasticsearch is reachable') {
        healthStatus.innerHTML = `<p>Status: ${data.status}</p><pre>${JSON.stringify(data.health, null, 2)}</pre>`;
    } else {
        healthStatus.innerHTML = `<p>Status: ${data.status}</p><p>Error: ${data.error}</p>`;
    }
})
.catch(error => {
    const healthStatus = document.getElementById('health-status');
    healthStatus.innerHTML = `<p>Error fetching health status: ${error.message}</p>`;
});
