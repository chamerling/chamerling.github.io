---
layout: page
title: Articles
---

<div id="posts"/>

<script src="/javascripts/jquery.js"></script>
<script src="/javascripts/underscore.js"></script>
<script src="/javascripts/gh3.js"></script>
<script>

	var cha = new Gh3.User("chamerling")
	,	branchContents = $("#posts");

	var chaBlog = new Gh3.Repository("articles", cha);
	chaBlog.fetch(function (err, res) {
		if(err) { throw "outch ..." }
		chaBlog.fetchBranches(function (err, res) {
			if(err) { throw "outch ..." }
			var master = chaBlog.getBranchByName("master");
			master.fetchContents(function (err, res) {
				if(err) { throw "outch ..." }
				master.eachContent(function (content) {
					branchContents.append('<article><h2 class="link-post"><a href="' + content.html_url + '">'  + content.name + '</a></h2></article>');
				});
			});
		})
	});
</script>
