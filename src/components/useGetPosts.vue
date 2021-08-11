<script>
import { ref } from 'vue'

async function fetchUsers(id) {
	let name = {}

	await fetch(`https://jsonplaceholder.typicode.com/todos/${id ? id : ''}`)
  .then(response => response.json())
  .then(json => {
		// console.log(json)
		return name = json
	})

	return name
}

export default function useGetPosts() {
  const repositories = ref({})

  const getPosts = async (params) => {
    const { id } = params
    repositories.value = await fetchUsers(id)

    console.log('repositories.value', repositories.value)
  }

  return {
    repositories,
    getPosts
  }
}
</script>