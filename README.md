function toggleInfo(itemId) {
  const header = document.querySelector(`[onclick="toggleInfo('${itemId}')"]`);
  if (!header) return;

  const item = header.closest('.info-item');
  if (!item) return;

  const isActive = item.classList.contains('active');
  const arrow = document.getElementById(`${itemId}-arrow`);
  const contentBox = document.getElementById(`${itemId}-box`);
  const content = document.getElementById(itemId);

  document.querySelectorAll('.info-item').forEach(i => {
    i.classList.remove('active');
    const innerArrow = i.querySelector('.info-arrow');
    if (innerArrow) innerArrow.style.transform = 'rotate(0deg)';
    const relatedBox = i.nextElementSibling;
    if (relatedBox && relatedBox.classList.contains('info-box')) {
      relatedBox.style.display = 'none';
    }
  });

  if (!isActive) {
    item.classList.add('active');
    if (arrow) arrow.style.transform = 'rotate(90deg)';

    if (contentBox) {
      contentBox.style.display = 'block';
      if (content) {
        content.style.display = 'block';
      }
      if (itemId === 'news-info' && content) {
        fetchNews();
      }
    }
  }
}
