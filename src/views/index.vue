<template>
	<div class="home">
		<canvas ref="$canvas"></canvas>
		<h1>青阳魂</h1>
		<h2>Passionate about technology & Hacker</h2>
		<ul>
			<li><router-link class="blog" :to="{ name: 'blog_index' }">Blog</router-link></li>
			<li><a class="github" target="_blank" href="https://github.com/luckyyyyy">GitHub</a></li>
			<li><a class="weibo" target="_blank" href="https://weibo.com/techvicky">WeiBo</a></li>
			<li><a class="zhihu" target="_blank" href="https://www.zhihu.com/people/qingyh/activities">知乎</a></li>
		</ul>
		<footer>
			<h3>Full Stack Developer</h3>
			<h4>C / Objective-C / JavaScript / PHP7 / MySQL / nodejs / ...</h4>
			<!-- <div><code>cm9vdEB3aWxsaWFtY2hhbi5tZQo=</code></div> -->
			<!-- <div><code>MTgwNTcxNzYwNTAK</code></div> -->
			<!-- <p>If you are interested in it, please let me know by my email.</p> -->
			<!-- <p>Copyright © 2017 William Chan. All Rights Reserved</p> -->
		</footer>
	</div>
</template>

<script>
	export default {
		mounted() {
			const $canvas = this.$refs.$canvas;
			const x = $canvas.getContext('2d');
			const pr = window.devicePixelRatio || 1;
			const w = window.innerWidth;
			const h = window.innerHeight;
			const f = 90;
			let r = 0;
			const u = Math.PI * 2;
			$canvas.width = w * pr;
			$canvas.height = h * pr;
			x.scale(pr, pr);
			x.globalAlpha = 0.6;
			let q;
			const y = (p) => {
				const t = p + (Math.random() * 2 - 1.1) * f;
				return (t > h || t < 0) ? y(p) : t;
			};
			const d = (i, j) => {
				x.beginPath();
				x.moveTo(i.x, i.y);
				x.lineTo(j.x, j.y);
				const k = j.x + (Math.random() * 2 - 0.25) * f;
				const n = y(j.y);
				x.lineTo(k, n);
				x.closePath();
				r -= u / -50;
				x.fillStyle = `#${(Math.cos(r) * 127 + 128 << 16 | Math.cos(r + u / 3) * 127 + 128 << 8 | Math.cos(r + u / 3 * 2) * 127 + 128).toString(16)}`;
				x.fill();
				q[0] = q[1];
				q[1] = { x: k, y: n };
			};
			const run = () => {
				x.clearRect(0, 0, w, h);
				q = [
					{ x: 0, y: h * 0.7 + f },
					{ x: 0, y: h * 0.7 - f },
				];
				while (q[1].x < w + f) {
					d(q[0], q[1]);
				}
			};
			document.onclick = run;
			document.ontouchstart = run;
			run();
		},
	};
</script>
