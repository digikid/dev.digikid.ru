<script setup lang="ts">
import { computed } from 'vue';

import { useData } from '@hooks/data';

import UISection from '@components/ui/UISection.vue';
import ListEducation from '@components/list/ListEducation.vue';

const { items: data } = useData<ExperienceData, ExperienceLocale>('education');

const items = computed<EducationItem[]>(() => {
  const main = data.value.filter((item) => item.id === 'main');
  const courses = data.value.filter((item) => item.id !== 'main').sort((a, b) => b.date - a.date);

  return [
    ...main,
    ...courses,
  ];
});
</script>

<template>
  <UISection
    id="education"
  >
    <div class="education">
      <ListEducation :items="items" />
    </div>
  </UISection>
</template>
