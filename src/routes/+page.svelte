<script>
	import '@fortawesome/fontawesome-free/css/all.min.css';
	import { cubicOut } from 'svelte/easing';
	import { circIn } from 'svelte/easing';
	import { fly } from 'svelte/transition';

	let isFocused = false;
	let isZoomed = false;
	$: zoomEffect = isZoomed ? 'transform: scale(1.2); transition: 0.2s ease-in-out;' : '';
	const pageNums = [1, 2, 3, 4];
	let selectedPageNum = 1;
	let selectedPageNumEffect = 'font-size: 18px; color: black; text-decoration-line: underline;';
	let isSideBarOpened = false;

	function handleMouseEnterType1() {
		isFocused = true;
	}

	function handleClick() {
		window.open('https://brunch.co.kr/brunchbook/aboutrelation');
	}

	function handleMouseOutType1() {
		isFocused = false;
	}

	function handleMouseEnterType2() {
		isZoomed = true;
	}

	function handleMouseOutType2() {
		isZoomed = false;
	}

	function clickLeftArrow() {
		selectedPageNum -= 1;
	}

	function clickRightArrow() {
		selectedPageNum += 1;
	}

	function clickPageNum(num) {
		selectedPageNum = num;
		console.log(num);
	}

	function openSideBar() {
		isSideBarOpened = true;
		console.log(isSideBarOpened);
	}

	function closeSideBar() {
		isSideBarOpened = false;
		console.log(isSideBarOpened);
	}
</script>

<header id="pageHead">
	<div class="header_inner">
		<div class="header_inner_left">
			<button id="btnMenu" type="button" class="fa-solid fa-bars fa-lg" on:click={openSideBar}
			></button>
			<h1>
				<a href="/" id="textLogo">brunch</a>
			</h1>
		</div>

		<div class="header_inner_right">
			<a href="/start" id="btnStart" on:click={() => alert('시작하기')}>시작하기</a>
			<button
				id="btnSearch"
				type="button"
				class="fa-solid fa-magnifying-glass fa-lg"
				on:click={() => alert('검색하기')}
			></button>
		</div>
	</div>
</header>

<main>
	<div class="main_inner" role="presentation" on:click={closeSideBar}>
		<article>
			<div class="intro">
				<h3 class="intro_title">작품이 되는 이야기, 브런치스토리<span id="iconLogo"></span></h3>
				<p class="intro_desc">
					<span
						>브런치스토리에 담긴 아름다운 작품을 감상해 보세요. <br /> 그리고 다시 꺼내 보세요.
						<br /></span
					> <span class="intro_desc_last">서랍 속 간직하고 있는 글과 감성을.</span>
				</p>
			</div>

			<div class="slide_wrap" style={selectedPageNum > 1 ? 'width: 100%' : ''}>
				<ul class="slide">
					<li class="slide_item" style="transform: translateX({(selectedPageNum - 1) * -100}%);">
						<div class="slide_item_grid">
							<div
								class="page1_item1"
								role="presentation"
								on:mouseenter={handleMouseEnterType1}
								on:click={handleClick}
								on:mouseleave={handleMouseOutType1}
							>
								{#if isFocused == true}
									<span class="focus_cover"></span>
								{/if}
								<span class="background_bottom"></span>
								<div class="book_cover">
									<div class="title_cover">
										<div class="book_title">
											<br />외지인에서현<br />지인으로강릉<br />에서살아남기
										</div>
										<div class="book_author"><br />상큼</div>
									</div>
									<div class="book_publisher">brunch book</div>
								</div>
								<div class="book_info">
									<strong class="edition_info">First Edition</strong>
									<div class="release_info">Released date.Sep.17.2023</div>
								</div>
							</div>
							<div
								class="page1_item2"
								role="presentation"
								on:mouseenter={handleMouseEnterType2}
								on:click={handleClick}
								on:mouseleave={handleMouseOutType2}
							>
								<div class="post_pic" style={zoomEffect}></div>
								<div class="post_cover">
									<strong class="post_title">미국에서도 공무원이<br />인기?</strong>
									<div class="post_author"><span class="post_author_by">by</span>coder</div>
								</div>
							</div>
							<div class="page1_item3"></div>
						</div>
					</li>
					<li
						class="slide_item"
						style="background-color: yellow; transform: translateX({(selectedPageNum - 1) *
							-100}%);"
					>
						2
					</li>
					<li
						class="slide_item"
						style="background-color: green; transform: translateX({(selectedPageNum - 1) * -100}%);"
					>
						3
					</li>
					<li
						class="slide_item"
						style="background-color: skyblue; transform: translateX({(selectedPageNum - 1) *
							-100}%);"
					>
						4
					</li>
				</ul>
			</div>

			{#if selectedPageNum > 1}
				<span class="slide_button_left_wrap" role="presentation" on:click={clickLeftArrow}>
					<span class="slide_button_left"></span>
				</span>
			{/if}
			{#if selectedPageNum < pageNums.length}
				<span class="slide_button_right_wrap" role="presentation" on:click={clickRightArrow}>
					<span class="slide_button_right"></span>
				</span>
			{/if}

			<div class="page_num">
				{#each pageNums as pageNum}
					{#if selectedPageNum == pageNum}
						<span
							role="presentation"
							on:click={() => clickPageNum(pageNum)}
							style={selectedPageNumEffect}>0{pageNum}</span
						>
					{:else}
						<span role="presentation" on:click={() => clickPageNum(pageNum)}>0{pageNum}</span>
					{/if}
				{/each}
			</div>
		</article>
	</div>
</main>

{#if isSideBarOpened}
	<aside
		in:fly={{ x: -100, easing: circIn }}
		out:fly={{ x: -100, duration: 2000, easing: cubicOut }}
	>
		<div class="sidebar_upper"></div>
		<div class="sidebar_bottom"></div>
	</aside>
{/if}

<style>
	header {
		display: block;
	}

	h1,
	h3 {
		display: inline-block;
		margin: auto;
	}

	button {
		background-color: transparent;
		border: 0;
		border-radius: 0;
		cursor: pointer;
		outline: none;
		vertical-align: middle;
		margin: 10px;
	}

	a {
		color: inherit;
		line-height: 0;
		overflow: hidden;
		text-indent: -9999px;
		text-decoration: none;
	}

	ul {
		padding: 0;
		margin: 0;
	}

	li {
		list-style: none;
		padding: 0;
		margin: 0;
	}

	aside {
		margin: auto;
		display: inline;
		position: fixed;
		width: 11%;
		height: 100%;
		float: left;
		top: 0px;
		z-index: 6;
		background-color: #fff;
		border-right: 1px solid #ddd;
	}

	.header_inner {
		margin: 30px 30px 0;
		display: flex;
		flex-wrap: wrap;
		align-items: center;
		justify-content: space-between;
	}

	.header_inner_left {
		display: flex;
		flex-wrap: wrap;
		align-items: center;
	}

	.intro_title {
		font-family: 'Nanum Myeongjo', sans-serif;
		letter-spacing: -0.05em;
		margin-bottom: 10px;
		color: #1a1a1a;
		font-size: 40px;
		font-weight: normal;
		text-align: left;
	}

	.intro_desc {
		font-family: 'Nanum Myeongjo', sans-serif;
		letter-spacing: -0.05em;
		color: #cacaca;
		font-size: 32px;
		line-height: 46px;
		margin-top: -3px;
	}

	.intro_desc_last {
		background: none;
		color: #dedede;
		display: inline;
	}

	.intro {
		margin: 0 auto;
		width: 960px;
	}

	.slide_wrap {
		position: relative;
		margin: 0 auto;
		width: 960px;
		height: 520px;
		overflow: visible;
		transition: 0.2s ease-in-out;
	}

	.slide {
		display: flex;
		overflow: hidden;
		width: 900%;
	}

	.slide_item {
		box-sizing: border-box;
		flex-shrink: 0;
		width: 960px;
		height: 520px;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: 0.2s ease-in-out;
	}

	.page1_item1 {
		position: absolute;
		width: 50%;
		height: 100%;
		background-image: linear-gradient(-180deg, #f4f4f4, #dedede 82%);
		justify-content: center;
		align-items: center;
		left: 0px;
		top: 0px;
		cursor: pointer;
	}

	.page1_item2 {
		position: absolute;
		width: 50%;
		height: 50%;
		justify-content: center;
		align-items: center;
		left: 50%;
		top: 0px;
		cursor: pointer;
		overflow: hidden;
	}

	.page1_item3 {
		position: absolute;
		width: 50%;
		height: 50%;
		background: skyblue;
		justify-content: center;
		align-items: center;
		left: 50%;
		top: 50%;
		cursor: pointer;
		overflow: hidden;
	}

	.focus_cover {
		background-image: url(https://t1.daumcdn.net/brunch9/static/images/pc/bg_bookblur.png),
			linear-gradient(-180deg, #bebebe, #bebebe 82%);
		position: absolute;
		width: 100%;
		height: 100%;
		z-index: 2;
		opacity: 0.7;
	}

	.background_bottom {
		display: block;
		background: #f6f6f6;
		width: 100%;
		height: 156px;
		position: absolute;
		bottom: 0;
	}

	.book_cover {
		position: absolute;
		background-image: url(https://img1.daumcdn.net/thumb/C460x648/?fname=http://t1.daumcdn.net/brunch/service/user/fH4x/image/RLaC-IP0SMvK55T8YyF4LwpTiL0.jpg);
		overflow: hidden;
		background-color: #ddd;
		background-position: 50% 50%;
		border-radius: 2px 6px 6px 2px;
		box-shadow: 0 10px 20px 0 rgba(0, 0, 0, 0.1);
		box-sizing: border-box;
		height: 324px;
		width: 230px;
		left: 50%;
		top: 95px;
		margin-left: -115px;
		padding: 68px 0 0;
		z-index: 2;
	}

	.title_cover {
		position: relative;
		background-color: #fff;
		height: 172px;
		width: 130px;
		margin: 0 50px;
		z-index: 3;
	}

	.book_publisher {
		bottom: 13px;
		color: #fff;
		display: block;
		font-family: 'SF Pro Bold', 'Malgun Gothic';
		font-size: 11px;
		left: 0;
		letter-spacing: 0.2px;
		line-height: 18px;
		position: absolute;
		text-align: center;
		width: 100%;
		z-index: 2;
	}

	.book_title {
		position: absolute;
		width: 100%;
		font-family: 'Nanum Myeongjo', sans-serif;
		text-overflow: ellipsis;
		font-size: 18px;
		font-weight: normal;
		line-height: 24px;
		max-height: 92px;
		padding: 0px 13px 0 10px;
		word-break: keep-all;
	}

	.book_author {
		position: absolute;
		bottom: 20px;
		color: #666;
		font-size: 11px;
		left: 0;
		padding: 0 10px;
		width: 100%;
	}

	.book_info {
		height: 78px;
		width: 100%;
		position: absolute;
		bottom: 0;
		z-index: 2;
		text-align: center;
		vertical-align: middle;
	}

	.release_info {
		position: relative;
		color: #959595;
		letter-spacing: -0.1px;
	}

	.post_pic {
		background-image: url(https://img1.daumcdn.net/thumb/C480x260.fjpg/?fname=https://t1.daumcdn.net/section/oc/d93f3fa190a94ec2a627deb9e77a9104);
		position: relative;
		width: 100%;
		height: 100%;
	}

	.post_cover {
		position: relative;
		width: 100%;
		height: 100%;
		top: -100%;
		background-color: #1a1a1a;
		opacity: 70%;
	}

	.post_title {
		display: block;
		position: relative;
		height: 50%;
		font-family: 'Nanum Myeongjo', sans-serif;
		font-size: 28px;
		font-weight: normal;
		letter-spacing: -0.025em;
		line-height: 36px;
		padding-top: 15%;
		color: #fff;
		text-align: center;
		justify-content: center;
	}

	.post_author {
		position: relative;
		color: #fff;
		width: 100%;
		font-family: 'Noto Sans Light', sans-serif;
		text-align: center;
	}

	.post_author_by {
		font-family: Georgia, sans-serif;
		font-style: italic;
	}

	.slide_button_left_wrap {
		position: relative;
		width: 90px;
		height: 90px;
		top: -285px;
		margin-left: 20px;
		background-color: #fff;
		border-radius: 50%;
		cursor: pointer;
		opacity: 80%;
		transition: 0.2s ease-in-out;
	}

	.slide_button_left {
		position: absolute;
		width: 60px;
		height: 50px;
		top: 20px;
		left: 15px;
		background: url(https://t1.daumcdn.net/brunch9/static/images/pc/ico_brunch_v9_230901.png)
			no-repeat 0 -50px;
	}

	.slide_button_right_wrap {
		float: right;
		position: relative;
		width: 90px;
		height: 90px;
		top: -285px;
		margin-right: 20px;
		background-color: #fff;
		border-radius: 50%;
		cursor: pointer;
		opacity: 80%;
		transition: 0.2s ease-in-out;
	}

	.slide_button_right {
		position: absolute;
		width: 60px;
		height: 50px;
		top: 20px;
		right: 15px;
		background: url(https://t1.daumcdn.net/brunch9/static/images/pc/ico_brunch_v9_230901.png)
			no-repeat -60px -50px;
	}

	.page_num {
		position: absolute;
		margin-top: 30px;
		width: 100%;
		height: 50px;
		text-align: center;
		font-family: 'Noto Sans DemiLight', 'Malgun Gothic', sans-serif;
	}

	.page_num span {
		font-size: 10px;
		color: #cacaca;
		margin-left: 10px;
		margin-right: 10px;
		cursor: pointer;
	}

	.sidebar_upper {
		background: #f8f8f8;
		height: 251px;
		border-bottom: 1px solid #ddd;
	}

	#pageHead {
		height: 60px;
	}

	#btnMenu {
		background-position: 0 -30px;
	}

	#textLogo {
		background: url(https://t1.daumcdn.net/brunch9/static/images/pc/logo_brunch_v1_221221.png);
		background-position: 0 80px;
		display: block;
		height: 22px;
		margin-top: -1px;
		width: 120px;
	}

	#btnStart {
		border: 1px solid #959595;
		border-radius: 15px;
		color: #666;
		font-family: 'Noto Sans Light', sans-serif;
		font-size: 15px;
		margin-top: -5px;
		text-align: center;
		text-decoration: none;
		padding: 5px 15px 5px 15px;
	}

	#iconLogo {
		background: url(https://t1.daumcdn.net/brunch9/static/images/pc/ico_brunch_v9_230901.png)
			no-repeat 0 0;
		display: inline-block;
		background-position: -80px -230px;
		height: 40px;
		margin: 1px 6px 0 5px;
		width: 40px;
	}
</style>
