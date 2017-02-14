# livereload-xl

This is a modified version of the package [node-livereload](https://github.com/napcs/node-livereload). It adds the ability to add a list of files and fire a callback when the files where changed.

There are no default watch options in this codebase.

Example:

```javascript
const path = require('path');
const liveReload = require('livereload-xl');

const root = path.resolve('~/test');

const files = [
	path.join(root, '**/*.md'),
	path.join(root, 'specificScript.js')
];

const liveReloadServer = liveReload.createServer({
	port: liveReloadPort
});

const handleChanges = changedFile => {
	files.forEach(filePattern => {
		const match = minimatch(changedFile, filePattern, {
			matchBase: true,
			dot: true
		});

		if (match) {
			const shortPattern = path.relative(root, filePattern);
			console.log(`Watched file change: ${changedFile} matched: ${shortPattern}`);

			liveReloadServer.refresh(changedFile);
		}
	});
};

liveReloadServer.watch(watchList, handleChanges);
```

