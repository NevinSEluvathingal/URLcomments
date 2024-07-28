<html >
<head>
    <style>
        h1, h2, h3, h4 {
            border-bottom: 0;
        }
    </style>
    <title>URL Comments</title>
</head>
<body>
    <h1>URL Comments</h1>

    <h2>Overview</h2>
    <p>URL Comments is a tool designed to enable users to comment on any website, even those where the comment section is disabled. This initiative aims to promote democratic discussion and enhance community interaction across the web.</p>

    <h2>Features</h2>
    <ul>
        <li><strong>Inject Custom Comment Section:</strong> Automatically adds a custom comment section to websites with disabled comments.</li>
        <li><strong>User-Friendly Interface:</strong> Mimics the look and feel of native comment sections, providing a seamless user experience.</li>
        <li><strong>Real-Time Commenting:</strong> Users can add, view, and manage comments directly on the page.</li>
        <li><strong>No Borders for Input:</strong> Customizable input field without borders for a clean look.</li>
        <li><strong>Color Scheme:</strong> Customizable color scheme for better integration with the website's design.</li>
    </ul>

    <h2>Installation</h2>
    <ol>
        <li>
            <strong>Clone the Repository</strong>
            <pre><code>git clone https://github.com/yourusername/url-comments.git</code></pre>
        </li>
        <li>
            <strong>Navigate to the Directory</strong>
            <pre><code>cd url-comments</code></pre>
        </li>
        <li>
            <strong>Load the Extension in Chrome</strong>
            <ul>
                <li>Open Chrome and navigate to <code>chrome://extensions/</code>.</li>
                <li>Enable "Developer mode" in the top right corner.</li>
                <li>Click "Load unpacked" and select the directory containing your extension files.</li>
            </ul>
        </li>
    </ol>

    <h2>Usage</h2>
    <p>Once the extension is loaded, it will automatically detect pages where the comment section is disabled and inject a custom comment section. Users can then add their comments, which will be displayed in the new section.</p>

    <h3>Injected Comment Section</h3>
    <ul>
        <li><strong>Add Comments:</strong> Users can write comments in a borderless input field.</li>
        <li><strong>Post Comments:</strong> Click the "Post Comment" button to add the comment to the page.</li>
        <li><strong>View Comments:</strong> All posted comments will be displayed in the comments container.</li>
        <li><strong>Clear Input:</strong> The input field is cleared after posting a comment.</li>
    </ul>

    <h2>Code</h2>
    <pre><code>
function injectCommentSection() {
  const observer = new MutationObserver((mutations) => {
    mutations.forEach((mutation) => {
      if (mutation.type === 'childList' && mutation.addedNodes.length) {
        const commentsDisabledMessage = document.querySelector('yt-formatted-string#message');
        const message = document.getElementById('message');

        if (commentsDisabledMessage && commentsDisabledMessage.textContent.includes('Comments are turned off')) {
          // Check if the custom comment section already exists
          if (!document.getElementById('custom-comment-section')) {
            const commentSection = document.createElement('div');
            commentSection.id = 'custom-comment-section';
            message.style.display = 'none';
            commentSection.innerHTML = `
              <h3>Comments</h3>
              <input style="background-color: rgb(1,1,1,0); border: none; width: 10rem; color: white;" id="comment-input" placeholder="Write a comment..."></input>
              <button id="post-comment">Post Comment</button>
              <div id="comments-container" style="color: white;"></div>
            `;
            commentsDisabledMessage.parentElement.appendChild(commentSection);

            document.getElementById('post-comment').addEventListener('click', () => {
              const comment = document.getElementById('comment-input').value;
              if (comment) {
                const commentContainer = document.getElementById('comments-container');
                const commentElement = document.createElement('p');
                commentElement.textContent = comment;
                commentContainer.appendChild(commentElement);
                document.getElementById('comment-input').value = '';
              }
            });

            observer.disconnect();  // Stop observing once the comment section is added
          }
        }
      }
    });
  });

  observer.observe(document.body, { childList: true, subtree: true });
}

injectCommentSection();
    </code></pre>

    <h2>Contributing</h2>
    <ol>
        <li><strong>Fork the Repository:</strong> Click on the "Fork" button at the top right corner of the repository page.</li>
        <li><strong>Create Your Feature Branch:</strong>
            <pre><code>git checkout -b feature/AmazingFeature</code></pre>
        </li>
        <li><strong>Commit Your Changes:</strong>
            <pre><code>git commit -m 'Add some AmazingFeature'</code></pre>
        </li>
        <li><strong>Push to the Branch:</strong>
            <pre><code>git push origin feature/AmazingFeature</code></pre>
        </li>
        <li><strong>Open a Pull Request:</strong> Navigate to your forked repository and click on the "New pull request" button.</li>
    </ol>

    <h2>License</h2>
    <p>This project is licensed under the MIT License - see the <a href="LICENSE">LICENSE</a> file for details.</p>
</body>
</html>
