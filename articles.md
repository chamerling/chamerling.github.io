---
layout: page
title: Articles
---

<ul class="posts">
</ul>

<script src="/javascripts/jquery.js"></script>
<script src="/javascripts/underscore.js"></script>
<script src="/javascripts/gh3.js"></script>
<script>

	var cha = new Gh3.User("chamerling")
	,	branchContents = $("ul");

	var chaBlog = new Gh3.Repository("articles", cha);
	chaBlog.fetch(function (err, res) {
		if(err) { throw "outch ..." }
		chaBlog.fetchBranches(function (err, res) {
			if(err) { throw "outch ..." }
			var master = chaBlog.getBranchByName("master");
			master.fetchContents(function (err, res) {
				if(err) { throw "outch ..." }
				master.eachContent(function (content) {
					branchContents.append('<li><a href=\"' + content.html_url + '\">'+content.name+'</a>');
				});
			});
		})
	});
</script>
