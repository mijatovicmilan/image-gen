---
name: image-gen
description: Generate or edit images with Codex's built-in $imagegen skill. Use for /image-gen or when the user asks to generate or edit an image.
argument-hint: <what to draw>
---

Send the user's request to Codex unchanged (Bash timeout 600000 ms).
If the user gives existing images to edit or use as reference, add --image <absolute path> for each.

log=$(mktemp "${TMPDIR:-/tmp}/image-gen.XXXXXX")
codex exec --sandbox read-only --skip-git-repo-check [--image <path>] <<'EOF' 2>"$log" && rm -f "$log" || { echo "Codex failed (exit $?). Last lines of $log:"; tail -n 20 "$log"; }
$imagegen <user's request>

Reply with the absolute path of each image.
EOF

Keep the heredoc: without input on stdin, codex exec waits for it and hangs.

Check that each returned file exists. If generation failed or a file is missing, report the error and do not retry.
If the output starts with "Codex failed", show the user the error from those log lines. "401 Unauthorized" means Codex isn't logged in: tell them to run `codex login`.

Show every image in chat with SendUserFile (display: render) if available; otherwise give a clickable link to each file.
SendUserFile previews only files inside the session's folders or scratchpad, so first copy each image into your scratchpad directory (if you have one) and send the copy.

Images stay where Codex saved them. Copy them elsewhere only if the user asks for them to be saved or used somewhere (for example on a site or in app); then put them where that use needs them.
