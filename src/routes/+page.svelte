<script>
    import { Dropzone } from 'flowbite-svelte';
    import ButtonDropdown from '../lib/Shared/ButtonDropdown.svelte'
  
    // @ts-ignore
    /**
	 * @type {any[]}
	 */
    let value = [];
    // @ts-ignore
    const dropHandle = (event) => {
      value = [];
      event.preventDefault();
      if (event.dataTransfer.items) {
        // @ts-ignore
        [...event.dataTransfer.items].forEach((item, i) => {
          if (item.kind === 'file') {
            const file = item.getAsFile();
            value.push(file.name);
            // @ts-ignore
            value = value;
          }
        });
      } else {
        // @ts-ignore
        [...event.dataTransfer.files].forEach((file, i) => {
          value = file.name;
        });
      }
    };
  
    // @ts-ignore
    const handleChange = (event) => {
      const files = event.target.files;
      if (files.length > 0) {
        value.push(files[0].name);
        // @ts-ignore
        value = value;
      }
    };
  
    // @ts-ignore
    const showFiles = (files) => {
      if (files.length === 1) return files[0];
      let concat = '';
      // @ts-ignore
      files.map((file) => {
        concat += file;
        concat += ',';
        concat += ' ';
      });
  
      if (concat.length > 40) concat = concat.slice(0, 40);
      concat += '...';
      return concat;
    };
  </script>
  
  <div>
    <ButtonDropdown title={"Saved"}></ButtonDropdown>

    <Dropzone
    id="dropzone"
    on:drop={dropHandle}
    on:dragover={(event) => {
      event.preventDefault();
    }}
    on:change={handleChange}>
    <svg aria-hidden="true" class="mb-3 w-10 h-10 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" /></svg>
    {#if value.length === 0}
      <p class="mb-2 text-sm text-gray-500 dark:text-gray-400"><span class="font-semibold">Click to upload</span> or drag and drop</p>
      <p class="text-xs text-gray-500 dark:text-gray-400">JSON Template</p>
    {:else}
      <p>{showFiles(value)}</p>
    {/if}
  </Dropzone>
  </div>
  

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
