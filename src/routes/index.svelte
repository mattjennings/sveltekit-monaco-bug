<script>
  import { onMount } from "svelte";

  let divEl;

  onMount(async () => {
    const Monaco = await import("monaco-editor");
    const jsonWorker = await import(
      "monaco-editor/esm/vs/language/json/json.worker?worker"
    ).then((res) => res.default);

    self.MonacoEnvironment = {
      getWorker: function () {
        return new jsonWorker();
      },
    };

    const editor = Monaco.editor.create(divEl, {
      value: JSON.stringify(
        {
          something: 123,
        },
        null,
        "\t"
      ),
      language: "json",
      automaticLayout: true,
    });

    return () => {
      editor.dispose();
    };
  });
</script>

<div bind:this={divEl} />

<style>
  div {
    height: 100vh;
  }
</style>
