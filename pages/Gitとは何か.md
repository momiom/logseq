- 分散型バージョン管理システム
	- > Git is a [free and open source](https://git-scm.com/about/free-and-open-source) distributed version control system designed to handle everything from small to very large projects with speed and efficiency.
		- https://git-scm.com
	- 参加者全員がプロジェクトの完全なコピーを持つ
		- だから分散という
		- GitHub中心のプロジェクトに関わっていると、中央集権的なシステム（クラサバの管理システム）感覚になるが、実際はGitHubは（すごい優秀な）参加者の一人に過ぎない
		- なので、ある日GitHubが消えても大丈夫（データはね。。issue、PR は消え去る）
	- ハッシュ木（マークル木）を用いて高速に動く
		- あるオブジェクトのハッシュ同士を結合してさらにハッシュを求める
		  ```
		             A+B+C+D
		             /     \
		           A+B      C+D
		          /  \      /  \
		         A    B    C    D
		  ※A~D はオブジェクトのハッシュ
		  ```
		- P2P（torrent のファイルの整合性チェックとかに使われている）
		- 仕組み的にA~Dのどれかひとつでも変更されれば連鎖的にハッシュが変わるので、ファイルの変更検知に使える
		- 余談
			- このハッシュを連鎖的に利用する仕組みはブロックチェーンと全く同じ
			- ブロックチェーンってすごいぜと言っているのに上記のハッシュの話しかしない人は、本質が全然わかってない。
			- ブロックチェーンは2018年に論文が発表された。
			- ハッシュ木は1979年にラルフ・マークルによって発明されている。
			- ブロックチェーンは分散型台帳としてお金のやりとりができるほどにセキュアである点がすごいのであって、ハッシュ木は既存の手段に過ぎない。
	- 差分を管理しない
		- だから早い
			- 2014/8 にコミットされた履歴が一瞬で出てくる（`git log --reverse`）
		- Gitは差分を管理しない
			- コミット毎に効率的なスナップショットを（そのときの状態をまるごと）持っている
			- [コミットはスナップショットであり差分ではない - GitHubブログ](https://github.blog/jp/2021-01-06-commits-are-snapshots-not-diffs/)
	- リーナス・トーバルズ（Linux作った人）がバージョン管理に困って2週間で作った
		- > The first version of git was just ~1300 lines of code, and I have reason 
		  to believe that I started it at or around April 3rd. The reason: I made 
		  the last BK release on that day, and I also remember aiming for having 
		  something usable in two weeks.
		  And hosting git itself was not that important for me - hosting the kernel 
		  was. And the first kernel commit was April 16 (with the first merges being 
		  a few days later). Which meshes with my "two week goal" recollection.
		  gitの最初のバージョンは、たった1300行のコードでした。4月3日に最後のBK（VCSのひとつ）のリリースを行ったので、その頃から作り始めたのでしょう。また、2週間で使えるようにすることを目標にしたことを覚えています。
		  git 自体のホスティングは私にとってはそれほど重要ではなく、カーネルをホスティングすることが重要でした。そして、最初のカーネルコミットは4月16日でした(最初のマージはその数日後)。これは、私の「2週間の目標」という記憶と一致しています。
			- https://marc.info/?l=git&m=117254154130732
		-