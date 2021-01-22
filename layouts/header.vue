<template>
  <header class="bg-gray-50 flex flex-col py-8 px-8">
    <div class="container flex flex-col">
      <h1 class="text-6xl font-extrabold text-gray-800">
        Quark language
      </h1>
      <p class="my-8 text-gray-500 text-lg">
        Quark is an Lisp programming language which can be either interpreted or compiled. It's dynamically and strongly typed and written in Typescript and Quark itself. Compiler output low-level C code.
      </p>
      <div class="container flex flex-row space-x-4">
        <button class="bg-indigo-500 hover:bg-indigo-600 transition-colors duration-300 py-3 px-8 text-white font-bold rounded-md flex flex-row items-center">
          <img src="~/assets/logo_dark.png" class="object-cover w-5 mr-2" />
          Download
        </button>
        <button class="bg-gray-100 py-3 px-8 text-gray-600 font-bold rounded-md w-36">
          Github
        </button>
      </div>
      <div class="container flex flex-col mt-16 mb-8">
        <code class="bg-gray-800 p-8 rounded-xl text-white">
          <pre>
  (let welcome (fn (username) {
    (print "Hello" (+ username "!"))
  }))

  (let name "Thomas")
  (welcome name)</pre>
        </code>
      </div>
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
