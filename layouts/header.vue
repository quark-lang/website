<template>
  <header class="bg-white py-8">
    <div class="container px-12">
      <h1 class="font-extrabold text-5xl text-gray-700">
        Quark
      </h1>
      <p class="text-gray-600 text-opacity-75 mt-2">
        Quark is an interpreted <b>Lisp programming language</b> written in Typescript which is focused on <b>productivity</b>, <b>speed</b> and <b>usability</b>.
      </p>
    </div>
    <code class="m-4 whitespace-pre-line">
      <pre class="bg-gray-800 py-10 mx-12 leading-7 text-gray-100 text-opacity-75 rounded-2xl shadow-lg">
        (let username "Thomas")
        (let welcome (fn (username) {
          (print "Hello" (+ username "!"))
        }))
        (welcome username)</pre>
    </code>
    <div class="flex flex-row px-12 space-x-2">
      <button class="bg-purple-600 text-opacity-90 text-white font-semibold py-2 px-6 rounded-md">
        Download
      </button>
      <button class="bg-transparent border-purple-600 border text-purple-700 py-2 px-9 rounded-md">
        GitHub
      </button>
    </div>
  </header>
</template>

<script>
export default {
  name: "header.vue",
  mounted() {
    const codes = document.getElementsByTagName('code');
    for (const code of codes) {
      const content = code.children[0].innerHTML;
      let state = '';
      const string = [...content].map((char) => {
        if (char === '"' && state === '') {
          state = 'STRING';
          return '<span class="text-green-600">"';
        } else if (char === '"' && state === 'STRING') {
          state = '';
          return '"</span>';
        }
        return char;
      }).join('');
      const brackets = string
        .replaceAll('(', '<span class="text-purple-600">(</span>')
        .replaceAll(')', '<span class="text-purple-600">)</span>')
        .replaceAll('{', '<span class="text-purple-500">{</span>')
        .replaceAll('}', '<span class="text-purple-500">}</span>');
      const keywords = brackets
        .replaceAll('print', '<span class="text-purple-300">print</span>')
        .replaceAll('let', '<span class="text-purple-300">let</span>')
        .replaceAll('fn', '<span class="text-purple-300">fn</span>')
        .replaceAll('+', '<span class="text-purple-300">+</span>')

      code.children[0].innerHTML = keywords;
    }
  }
}

</script>
