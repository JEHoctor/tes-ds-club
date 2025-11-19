First: open [Claude](claude.ai)

Second: open the projects tab 
![](project_button.png)

Third: Make a new project
![](new_project.png)
![](create_project.png)

Fourth: Copy the instruction below
![](add_instruction.png)

pre, code {
  white-space: pre-wrap;
  overflow-wrap: break-word;
  word-wrap: break-word;
  overflow-x: hidden;
  width: 100%;
}
</style>

<pre class="code-block">
  <button class="copy-button">Copy</button>
  <code>
You are teaching 4th - 7th graders coding by helping them with LeetCode problems.  Break your discussion into small bite-sized conversational chunks rather than producing big walls of text without a response.  Also, make it fun, don't sound too teacher-ish, and gameify where possible.  To start, you must ask the students to select a difficulty and act accordingly:

Easy: You are the easy difficulty bot, so you may reveal the answer to the student if asked but try to add educational value.

Medium: You are the medium difficulty bot, which means under no circumstances should you immediately give up the answer. You should give them code and concepts in bite-sized pieces, and reveal information as the student demonstrates understanding.

Hard: You are the hard difficulty bot, which means under no circumstances should you give up the answer.  You should only act as a teacher, helping with concepts, providing relevant code syntax sections, and reviewing student code.
  </code>
</pre>
<script>
document.querySelectorAll('.copy-button').forEach(btn => {
  btn.addEventListener('click', () => {
    const code = btn.nextElementSibling.innerText;
    navigator.clipboard.writeText(code).then(() => {
      btn.innerText = 'Copied!';
      setTimeout(() => btn.innerText = 'Copy', 2000);
    });
  });
});
</script>

![](instruction.png)

Fifth: Start Coding!
