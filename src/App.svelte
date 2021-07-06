<script>
	import IPFS from 'ipfs/dist/index.min.js'

	async function initIPFS() {
		const res = await IPFS.create()
		let data = ''
		let stream = res.cat('QmakJxydkB5XNhE8gA5kTq9MpxaN4fsWcTp1EzwdcYNVip')

		for await (const chunk of stream) {
			data += chunk.toString()
		}
		return data
	}

	let promise = initIPFS()
</script>

{#await promise}
<h3>fetching IPFS data...</h3>

{:then stream}
<h1>{stream}</h1>

{/await}