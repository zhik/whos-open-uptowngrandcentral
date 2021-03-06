<script>
    import SlimSelect from './SlimSelect.svelte'
    import CategoryFilterButtons from './CategoryFilterButtons.svelte'
    import {rows, filters} from '../../../stores'
    import {categoryGroups, styles} from '../../../constants'

    let selectedCategories = []
    let categoryOptions

    let selectedSubCategories = []
    let subCategoryOptions

    $: setupCategoryOptions($rows)

    function setupCategoryOptions(rows) {
        if (rows.length > 0) {
            //reset
            selectedCategories = []
            //set up SlimSelect options
            let options = categoryGroups.reduce((groups, groupLabel) => {
                const options = styles
                        .filter(cat => cat.group === groupLabel)
                        .map(cat => ({
                            text: cat.categoryName,
                            value: cat.categoryName,
                            color: cat.fillColor,
                            innerHTML: `<span style="padding-left: 5px; border-left: 5px solid ${cat.fillColor};">${cat.categoryName}</span>`
                        }))

                const uniqueOptions = options.filter((item1, index, self) => {
                    const findIndex = self.findIndex(item2 => item1.text === item2.text)
                    return findIndex === index
                })

                const group = {
                    label: groupLabel,
                    options: uniqueOptions
                }

                return [...groups, group]
            }, [])

            //get unique categories from rows
            const uniqueCategories = Array.from(new Set(rows.map(({Category}) => Category)))
            //filter for items not in groups
            const otherGroup = uniqueCategories.filter(cat => !styles.map(i => i.categoryName).includes(cat))

            categoryOptions = {
                data: [...options, {
                    label: 'Other',
                    options: otherGroup.map(cat => ({text: cat, value: cat}))
                }]
            }
        }
    }

    $: setupSubCategoryOptions($rows, selectedCategories)

    function setupSubCategoryOptions(rows, selectedCategories) {
        if (rows.length > 0 && selectedCategories) {
            //reset
            selectedSubCategories = []
            const subCategories = rows.filter(({Category}) => selectedCategories.includes(Category))
                    .map(c => c['Sub-Category'])
                    .reduce((a, c) => {
                        //split by comma
                        return [...a, ...c.split(',')]
                    }, [])
                    .sort((a, b) => a.localeCompare(b))
            const uniqueSubCategories = Array.from(new Set(subCategories))
            subCategoryOptions = {data: uniqueSubCategories.map(c => ({text: c, value: c}))}
        }
    }

    $: {
        if ($filters) {
            //remove existing filter
            const _filters = $filters
            const filter = _filters.findIndex(f => f.label === 'categories')
            if (filter > -1) _filters.splice(filter, 1)
            //generate new filter
            if(selectedCategories || selectedSubCategories){
                const categoryFilter = {
                    label: 'categories',
                    filter: (row) => {
                        if (selectedCategories.length) {
                            if (selectedSubCategories.length) {
                                return selectedCategories.includes(row.Category) && row['Sub-Category'].includes(selectedSubCategories)
                            } else {
                                return selectedCategories.includes(row.Category)
                            }
                        } else {
                            return true
                        }
                    }
                }
                filters.set([..._filters, categoryFilter])
            }
        }
    }

</script>

{#if categoryOptions && 'data' in categoryOptions}
    <CategoryFilterButtons bind:value={selectedCategories} options={categoryOptions} text="Categories"/>
{/if}


{#if subCategoryOptions && 'data' in subCategoryOptions && subCategoryOptions.data.length}
    <SlimSelect bind:value={selectedSubCategories} options={subCategoryOptions} multiple={true}
                text="Sub Categories"/>
{/if}


<style>
    :global(.ss-value) {
        background-color: #878787 !important;
        font-weight: 500;
    }

    :global(span.ss-disabled) {
        font-size: 0.8em !important;
        color: rgba(113, 113, 113, 0.8) !important;
    }
</style>